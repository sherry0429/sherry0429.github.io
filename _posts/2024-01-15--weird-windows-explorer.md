# windows底部的bar（资源管理器）无法点击的问题解决

自从升了几次windows之后，底部的资源管理器经常出现无法点击的情况，一直点击它，就会重启。

重启结束之后，可以恢复一会，然后就又寄了。


历经折腾，搞定了。

## 1.重启explorer.exe

打开任务管理器，搜索explorer.exe，点击重新启动。

这会恢复一小阵，让你可以进行一些操作，比如，打开windows资源管理器

## 2. 替换explorer.exe

1. 找其他好的系统里面的，C://windows/explorer.exe，
2. 在你有问题电脑的C://windows/下创建一个tmp目录，然后把这个另一个电脑的explorer.exe复制到你有问题电脑的C://windows/tmp/explorer.exe，
3. 右键你电脑里的explorer.exe，调整它的权限（不调整的话，默认是属于TrustInstaller，这样就不对。应该调整为Adminstrator完全控制），具体参考这里https://zhuanlan.zhihu.com/p/108569823
4. 调整好后，把tmp下其他机器的explorer.exe，复制到C://windows/下，覆盖掉你自己的explorer.exe（只有进行过第三步，你才会有权限这么做）

## 3. 重新运行explorer.exe

1. 打开任务管理器，（ctrl + windows + del），找到“windows资源管理器”，右键结束任务
2. 这时候你下面的bar没了，不要慌张
3. 在任务管理器左上角点击文件->运行新任务
4. 输入explorer.exe
5. 如果步骤一切正确，这时候底下的bar又出现了，也不会再卡死了。

问题的底层原因应该是权限问题，windows explorer.exe的权限和其他权限冲突导致的卡死。

