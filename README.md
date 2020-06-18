# QQ刷屏助手

## 代码

```python
# 原理是先将需要发送的文本放到剪贴板中，然后将剪贴板内容发送到qq窗口
# 之后模拟按键发送enter键发送消息

print('代码来自CSDN，原为自动回复，经过更改，现支持刷屏并调整参数。')
print('本工具仅适用于PCQQ和TIM（不包含QQUWP）！')
print('请在使用前确保发送快捷键为Enter！')
print('请在使用前打开目标用户的聊天窗口！')
print('请在使用前确认剪切板中没有重要内容，否则会被覆盖！')

import easygui
import time
import win32gui
import win32con
import win32clipboard as w

def getText():
    """获取剪贴板文本"""
    w.OpenClipboard()
    d = w.GetClipboardData(win32con.CF_UNICODETEXT)
    w.CloseClipboard()
    return d

def setText(aString):
    """设置剪贴板文本"""
    w.OpenClipboard()
    w.EmptyClipboard()
    w.SetClipboardData(win32con.CF_UNICODETEXT, aString)
    w.CloseClipboard()

def send_qq(to_who, msg):
    """发送qq消息
    to_who：qq消息接收人
    msg：需要发送的消息
    """
    # 获取qq窗口句柄
    qq = win32gui.FindWindow(None, to_who)
    # 投递剪贴板消息到QQ窗体
    win32gui.SendMessage(qq, 258, 22, 2080193)
    win32gui.SendMessage(qq, 770, 0, 0)
    # 模拟按下回车键
    win32gui.SendMessage(qq, win32con.WM_KEYDOWN, win32con.VK_RETURN, 0)
    win32gui.SendMessage(qq, win32con.WM_KEYUP, win32con.VK_RETURN, 0)
    print('已发送消息（第%s条）'%ci)


# 主要
list=['目标聊天（窗口）','次数','内容']
lists=['昵称、群名或备注','10','消息内容']
listr=easygui.multenterbox(msg='欢迎使用QQ刷屏助手，填写内容请勿为空！', title='QQ刷屏助手', fields=list,values=lists)
to_who=listr[0]
set=int(listr[1])
msg=listr[2]
ci=1
# 将消息写到剪贴板
setText(msg)
while ci<=set:
    send_qq(to_who, msg)
    ci=ci+1
    time.sleep(0.05)

```



## 注意事项

- 该程序部分代码来自网络，由其他用户制作，原为自动回复，经更改后（详见“更改内容”）支持刷屏并调整参数。

- 该程序仅适用于PCQQ和TIM（不包含QQ UWP）！

- 使用前请打开目标聊天窗口并独立（不独立应该也行，但我不敢冒险，没试过）！

- 使用前请将发送快捷键设置为Enter！

  ## 更改内容

  保留发送、设置文字和获取文字方法，删去监测方法，添加循环调用和GUI界面。

  ## V1.0

  #### 如何使用？

  首先，特别是对于一个业余才写程序的学生来说，程序的开始一般都是黑底白字。

  然后填写参数即可刷屏。

  ## V2.0

  #### 更新内容

- TIM测试成功

- 增加可视化界面

  ![QQ刷屏助手V2.0](https://img-blog.csdnimg.cn/20200521221836812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3R0Njg2ODY=,size_16,color_FFFFFF,t_70#pic_center)

  看到这个界面大家就比较熟悉了吧？不用我多说什么了吧？

## 下载
2.0可以在[我的网盘](https://n802.com/dir/27256477-39300593-4f1b29)或存储库中下载，1.0不共享
