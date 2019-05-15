**我的应用场景：**

jenkins的master节点：centos6.8，有个项目需要用windows系统提供服务，所以添加了widows slave节点（win7），并在windows slave节点上安装好所需要的环境，
如maven、git、jenkin服务等。并在master节点上，通过label标签选择指定的windows slave节点运行执行项目。

**遇到的问题：**
    在使用jenkins打包时候，windows上编译生成了最新的target文件夹，但是jenkins打包完成后，windows上不能按预期出现项目启动窗口。

**解决问题：**
    通过查找，打包后jenkins条用bat脚本启动项目过程中，有个会话传递的过程。
    我使用的jenkins的master节点上执行打包操作，在windows slave节点上win7系统上运行此job，此为会话0.
    希望将执行的启动脚本，在win7上显示GUI窗口，此为会话1.
    需要借助psexec程序来完成会话传递过程。
    `psexec`工具路径:
        https://github.com/cxhzcxhz/Scattered-knowledge-points/blob/master/tools/PSTools.zip
我的配置如图：
    https://github.com/cxhzcxhz/Scattered-knowledge-points/blob/master/images/jenkins1.png
我的bat命令：
    D:\app\config-files\PSTools\psexec.exe -i 1 cmd /c start java -jar D:\app\flow-survey-report\flow-survey-report-1.0.0-SNAPSHOT.jar
jenkins执行完成，需要执行脚本时，如图：
    https://github.com/cxhzcxhz/Scattered-knowledge-points/blob/master/images/jenkins2.png
jenkins执行节本完成后，如图：
    https://github.com/cxhzcxhz/Scattered-knowledge-points/blob/master/images/jenkins3.png
此时在win7系统上出现了项目启动时的窗口。

参考链接:https://stackoverflow.com/questions/22602951/open-excel-on-jenkins-ci/22610664#22610664
