  [1]: assets/posts/javaee7����duke-forestʧ�ܵĽ������/examples.png
  [2]: assets/posts/javaee7����duke-forestʧ�ܵĽ������/pom.xml.png
  [3]: assets/posts/javaee7����duke-forestʧ�ܵĽ������/build-duke-forest.png



##  �������
	dukes-payment ..................................... FAILURE [4.308s]
	...
	Failed to execute goal org.codehaus.cargo:cargo-maven2-plugin:1.4.4:redeploy (deploy) on project dukes-store: 
	Execution deploy of goal org.codehaus.cargo:cargo-maven2-plugin:1.4.4:redeploy failed: 
	GlassFish admin command failed: asadmin exited 1 -> [Help 1]

##  ԭ��
���ڲ����ҵ�Glassfish����ȷ·�����µ�

##  �������
### NetBeans8.2
1. ����Ŀ` /javaee-tutorial/examples`
![��example][1]
2. ����Ŀ`javaeetutorial->��Ŀ�ļ�->pom.xml`
![��pom.xml][2]
3. �ҵ����ƴ���
        <profile>
            <id>windows</id>
            <activation>
                <os>
                    <family>windows</family>
                </os>
            </activation>
            <properties>
                <glassfish.home.prefix>c:/</glassfish.home.prefix>
                <glassfish.executables.suffix>.bat</glassfish.executables.suffix>
            </properties>
        </profile>
4.  �޸�Ϊ
        <profile>
            <id>windows</id>
            <activation>
                <os>
                    <family>windows</family>
                </os>
            </activation>
            <properties>
                <glassfish.home>${glassfish.home.prefix}/glassfish4</glassfish.home>
                <glassfish.home.prefix>c:/</glassfish.home.prefix>
                <glassfish.executables.suffix>.bat</glassfish.executables.suffix>
            </properties>
        </profile>
5.  ����JavaDB
6.  ����GlassFish Server
7.  ����Ҽ���Ŀ`dukes-forest`����
![����][3]
