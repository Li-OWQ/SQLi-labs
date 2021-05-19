## 目标

使用kali虚拟机搭建SQLi-labs靶场并将过程上传至github

### 第一步 准备搭建环境
   关于如何搭建虚拟环境 [百度](https://www.baidu.com/) 
   准备工具 kali虚拟机 git/github软件以及账户[官网地址](https://github.com/) SQLi-labs源代码[项目地址](https://github.com/mukkul007/sqli-labs-kali2)
   ### 第二步 使用git克隆源代码
   windows方法：进入搜索引擎搜索git安装  
   [官方下载地址](https://git-scm.com/)    
   linux方法：使用**终端**命令
     
	 sudo apt-get install git  
安装完成后，需要先完成对git的配置

	git config user.name "用户名"	
	git config user.email "邮箱"
	
现在已经可以克隆SQLi-labs源代码到本机中了

    cd /var/www/html/
	git clone https://github.com/mukkul007/sqli-labs-kali2 sqli-labs
	
![](https://z3.ax1x.com/2021/05/19/g5pNan.png)
	
### 第三步 搭建SQLi-labs练习环境
接下来开启kali的apache与mysql服务  

	sudo service apache2 start
	sudo service mysql start #初次使用可能会要求配置密码

在浏览器地址栏输入127.0.0.1出现以下画面![](https://z3.ax1x.com/2021/05/19/g5PjRx.png)

现在修改配置文件  将密码修改成自己设置的密码
	
	cd sqli-labs/
	cd sql-connections/
	vi db-creds.inc
![](https://z3.ax1x.com/2021/05/19/g5FY4A.png)

访问http://127.0.0.1/sqli-labs/ 点击setup完成安装  
![](https://z3.ax1x.com/2021/05/19/g5Eag1.png)

显示如图  
![](https://z3.ax1x.com/2021/05/19/g5Eq8s.png)  
到此搭建完成
### 第四步 上传到远程仓库
删除源代码中的仓库  
    
	cd /var/www/html/sqli-labs
	rm -rf .git  
下一步将源代码文件夹添加到暂存区并添加到本地仓库  
    
	cd ..
	git add sqli-labs/
	git commit -m "源代码"  
在github上建立远程仓库并与本机建立连接
![](https://z3.ax1x.com/2021/05/19/g5X77t.png)
生成SSH连接密钥
	
	ssh-keygen -t rsa -C "your_email@youremail.com"
在指定的保存路径下会生成2个名为id_rsa和id_rsa.pub的文件

![](https://z3.ax1x.com/2021/05/19/g5vtRU.png)

使用文本编辑器打开pub公钥 复制其中所有内容 进入github账户配置界面 选择SSH and GPG keys项 点击New SSH KEY粘贴即可

![](https://z3.ax1x.com/2021/05/19/g5vcRO.png)

连接到远程仓库并提交
		
		git remote add origin 你的github仓库地址
		git push origin master
提交完成如下图![](https://z3.ax1x.com/2021/05/19/g5OHWF.png)
