  [1]: /assets/posts/NetBeans快捷操作/封装字段.png
  [2]: /assets/posts/NetBeans快捷操作/组件面板.png
  [3]: /assets/posts/NetBeans快捷操作/清爽的URL设置.png

####  生成Getter和Setter方法

在源代码编辑器中右键单击名称字段，然后选择`重构>封装字段`。将打开`封装字段`对话框，其中列出了名称字段。
请注意，“字段的可观性”默认设置为private，“存取方法的可观性”设置为public，
表示类变量声明的访问修饰符将被指定为private，而getter和setter方法将使用public修饰符生成。

![封装字段][1]

####  组件面板

`Ctrl+Shift+8`

![组件面板][2]

####  清爽的URL设置

在`web.xml`文件中

![清爽的URL设置][3]

####  调用代码完成建议和文档支持，操作是下面其中之一

*  `Ctrl-Alt-空格键`
*  `Ctrl-空格键`

>   因为您使用的是 JSF 2.x，所以可以使用标注来声明所有 JSF 特定的组件。
在以前的版本中，您需要在 Faces 配置文件 (faces-config.xml) 中对其进行声明。
*  Tip: 是否不能自己创建faces-config.xml才能达到上述效果？

#### 脱离鼠标快捷键

 

* `ctrl + Tab`: 窗口选择
* `ctrl + Q`: 上一个编辑位置
* `ctrl + End`: 移动插入点至文档结尾
* `ctrl + UP`: 向上滚动
* `ctrl + DOWN`: 向下滚动
* `ctrl + E`: 删除行
* `ctrl + W || ctrl + F4`: 关闭窗口 
* `ctrl + G`: 转至行 (光标转到,但是编辑区域没有转到,则关闭文件再打开)

使用书签

* `Ctrl-Shift-M`: 开启/关闭书签
* `Ctrl-Shift-逗号`: 转至上一个书签
* `Ctrl-Shift-句点`: 转至下一个书签


#### 起始页

帮助 -> 起始页


#### 参考

* [NetBeans IDE Java编辑器中的代码帮助：参考指南](https://netbeans.org/kb/docs/java/editor-codereference.html#editor-features)