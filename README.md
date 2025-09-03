⚠️ **注意**，这一插件目前正在这一仓库被维护并更新更多功能：https://github.com/ret2ldz/KPwnHelper

[English](README.en.md) | [简体中文](README.md)

# Better printk for IDA
个人在使用IDA逆向内核模块的时候，由于printk格式的问题头疼很久，IDA无法自动识别，只能手动去数据区一个个字节看，很不直观且很麻烦，于是就有了这个插件。
本插件基于IDAPython9.0开发，且实测8.3版本也可以使用核心功能。实现了：
1. 分析内核驱动时自动在伪代码窗口与反汇编窗口生成printk的字符串和内核日志等级
2. 为IDA注册了新的数据类型`printk_str`，在数据界面对调用指针右键选择Better printk即可将其格式化输出。

# 使用方法
## Better Printk Output
将better_printk.py拷贝至`/$IDAdir(9.0)/plugins`目录下即可，插件会在反编译函数时自动工作，为伪代码窗口和反汇编窗口生成相关注释显示printk的内容和内核日志等级。
![better_printk](/assets/operation2.gif)

## Optimize printk str
右键单击数据窗口的字符串，直接转化为printk即可
![turn_data_into_printkstr](/assets/operation.gif)


# 注意事项/潜在BUG

1. 对于伪代码界面注释，IDA并没有提供一个很好的API，无法从地址匹配到伪代码行（对输出伪代码的操作只能是文本操作）。因此注释的匹配是按照IDA反编译函数的调用顺序来的，**如果**出现CTree中printk调用在前而伪代码界面包含printk的行在后，则注释的顺序会出现问题。此时参考汇编界面的优化输出即可。

2. 对于IDA版本在9.0以下的（作者个人有8.3版本），数据结构注册部分由于api的冲突存在问题，反编译hook部分可以正常使用（至少在8.3）

# 其他
本人制作此插件纯属心血来潮（没想到github上居然没有相关内容），欢迎各路师傅对此插件做优化修改或在其模板上进行二次开发。

感谢Cursor与deepseek-v3。
