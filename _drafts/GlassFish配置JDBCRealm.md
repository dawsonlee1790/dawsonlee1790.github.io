  [1]: /assets/posts/GlassFish配置JDBCRealm/我数据库的结构.png
  [2]: /assets/posts/GlassFish配置JDBCRealm/我的JDBCRealm配置.png

##  数据库结构
*  USERS表

CREATE TABLE USERS (
        USERID VARCHAR(50) NOT NULL,
        PASSWORD VARCHAR(128) NOT NULL
    );


*  GROUPS表

CREATE TABLE GROUPS (
        GROUPID VARCHAR(20) NOT NULL
    );


*  USERS_GROUPS联接表

CREATE TABLE USERS_GROUPS (
        GROUPID VARCHAR(20) NOT NULL,
        USERID VARCHAR(50) NOT NULL
    );

##  Glassfish JDBCRealm配置片段来自domain.xml

    <auth-realm name="MyRealm" classname="com.sun.enterprise.security.auth.realm.jdbc.JDBCRealm">
      <property description="null" name="jaas-context" value="jdbcRealm"></property>
      <property name="encoding" value="Hex"></property>
      <property description="null" name="password-column" value="PASSWORD"></property>
      <property name="datasource-jndi" value="jdbc/myDS"></property>
      <property name="group-table" value="USERS_GROUPS"></property>
      <property name="user-table" value="USERS"></property>
      <property description="null" name="group-name-column" value="GROUPID"></property>
      <property name="digest-algorithm" value="SHA-512"></property>
      <property description="null" name="user-name-column" value="USERID"></property>
    </auth-realm>

注意，该group-name-column属性的值为GROUPID，映射到GROUPID连接表的列USERS_GROUPS而不是组表GROUPS。
这是因为JDBCRealm发出以下SQL语句（如果您反编译com.sun.enterprise.security.auth.realm.jdbc.JDBCRealm该类）

密码查询，用户Id是从DigestLoginModule传递的参数：

	SELECT <passwordColumn> FROM <userTable> WHERE <userNameColumn> = ?；

组查询，用户ID作为参数传递：
	
	SELECT <groupNameColumn> FROM <groupTable> WHERE <groupTableUserNameColumn> = ?;

当您考虑第二个查询的结构时，很明显组表必须包含映射到组ID的用户ID（这会导致映射到多个组的用户的组数据重复），或者组表必须是将用户映射到组的连接表。



##  下面是我按照上述原理配置的JDBCRealm
*  我数据库的结构
![我数据库的结构][1]

*  我的JDBCRealm配置
![我的JDBCRealm配置][2]

** 注意：
>  JAAS Context 一定得填`jdbcRealm`，否则会报错

			javax.security.auth.login.LoginException:没有为 MyRealm  配置LoginModules 

>  `User Name Column`一定要填`user`表的主键（即`primerykey`）
>  `Group Table User Name Column`也一定要填组表（在这里指`group_has_user`表）关联到`user.id`的外键`group_has_user.id`
>  否则GlassFish服务器会报错`严重：jdbcrealm.grouperror`。即使不报错还是会导致*用户权限约束*失效


---

["参考"](https://stackoverflow.com/questions/6809081/glassfish-jdbc-realm-group-membership)

---