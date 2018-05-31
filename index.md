苹果官方给提供了xcodebuild和xrun shelll命令用来自动编译打包ipa功能。在使用之前必须要先安装command line tools才可以执行命令。command line tools的安装方式可以从官网下载，也可以直接用命令行进行安装，在终端输入(默认已经安装了Xcode):
```
xcode-select --install
```
安装完成之后就可以使用脚本命令来打包了。废话不多说，直接上代码。
```
project_path=$1
target_name=$2

cd $project_path

/usr/bin/xcodebuild -target $target_name clean
/usr/bin/xcodebuild -target $target_name

/usr/bin/xcrun -sdk iphoneos PackageApplication -v ./build/Release-iphoneos/$target_name.app -o $project_path/$target_name.ipa
```
简单说下这几句话的意思。 
第一二句是接收外部调用的参数，第一个参数是要编译的项目所在的路径（到xcodeproj文件上级目录）。第二个参数是target名称。 
打包编译要到项目所在路径进行，所以cd到project_path目录下。 
xcodebuild第一句话是用来clean之前编译生成的文件。 
xcodebuild第二句是编译工程这一步会生成target_name.app文件 
最后一步是把.app文件打包成.ipa文件。-v参数后面指向的是第二部编译出来的.app文件，-o后是生成的ipa文件输出路径

好了，就这样吧，自动打包本来也没多少东西。 
原文地址：http://blog.csdn.net/showhilllee/article/details/47001181 
欢迎留言讨论。

shell脚本地址：http://download.csdn.net/detail/showhilllee/8923171
