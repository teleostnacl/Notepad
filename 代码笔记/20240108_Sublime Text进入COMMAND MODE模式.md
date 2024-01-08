Sublime Text自带Vim模式，当按下`ESC`键之后就会进入`COMMAND MODE`模式，此时将无法进行任何输入。按`A` `I` `O` 三个按键中任何一个就可以回到`INSERT MODE`，也就是编辑模式。

Sublime Text可以关闭vim模式，进入settings，加入以下内容：
``` bash
// 关闭Vim模式，防止Sublime Text使用过程中进入Vim模式
"ignored_packages":
[
	"Vintage"
]
```
