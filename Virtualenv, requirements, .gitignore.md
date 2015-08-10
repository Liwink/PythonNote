##Virtualenv
1. 存在什么问题

	系统中的多个项目，可以需要不同的Python配置环境，例如A项目可能需要Django 1.5.0，而B项目需要Django 1.7.1。如果他们都共用系统的默认依赖包环境，操作会非常复杂

2. 如何解决的，提供了什么优化

	Virtualenv，可以封装每个项目的使用环境，为每个项目提供独立的第三方依赖服务。

3. 如何操作

	- 安装
	
		`pip install virtualenv`
	- 创建依赖环境
	
		`virtualenv venv  # venv为自定的环境名`
	
		venv创建后，可以在当前路径中看到venv文件夹，里面存放项目安装的依赖服务

	- 使用独立的venv环境
	
		`source venv/bin/activate`
	
	- 在venv环境中安装依赖服务

		`pip install django==1.5.0`
	
		这里安装删除都不需要sudo的权限
	
	- 关闭独立环境

		`deactivate`

## requirements

1. 存在什么问题
	
	每个项目都需要一定的依赖包、指定的第三方服务才能正常运行。在项目迁移变动时，依赖环境可能并不会随之迁移，所以项目需要重新建立所需环境

2. 如何解决
	
	pip可以记录项目中安装的第三方服务及其版本，并将他存放在requirements.txt中。
在项目迁移，失去原先的依赖环境后，可以通过pip安装requirements.txt中记录的第三方服务

3. 如何操作
	
	- pip将第三方服务记录到requirements.txt中
	
		`pip freeze > requirements.txt`

	- 在新环境中，安装requirements.txt中的第三方服务

		`pip install -r requirements.txt`

## .gitignore

1. 存在什么问题
	
	项目中可能存在一些不需上传的文件，例如Python编译时生成的.pyc等等，如果每次使用Git上传时手动剔除这些文件，过程会非常繁琐

2. 如何解决
	
	可以在项目中添加名为.gitignore的文件，其中记录了git添加项目时可以自动忽略的文件，这样使用`git add .`时，就会跳过那些文件。

3. 如何操作

	- 创建`.gitignore`，在项目根目录中
	- 在[网页](https://www.gitignore.io/)中根据项目环境，如操作系统，开发工具等自动生成gitignore资源
	- 将网页生成的文档，存储在本地的`.gitignore`中
	- `git add .`上传文件时，会自动忽略`.gitignore`中标注的文件。
