---
title: hexo在github上实现自动发布
date: 2020-07-20 18:05:12
tags:
---
### 前提描述

hexo 创建文档后需要将编译后的public目录提交到git线,git page  才能更新，所以有两条代码线，为了减少提交静态代码到git page的操作，通过git action 实现提交hexo代码后自动更新git page的代码

### hexo _config.yml修改配置

```
deploy:
  type: 'git'
  repo: git@github.com:xpfyg/xpfyg.github.io.git
  branch: master
```

### 添加密钥对

1.运行以下终端命令，将电子邮件替换为连接到您的GitHub帐户的电子邮件。

```
ssh-keygen -t rsa -C "997052247@qq.com"
```

2.出现的交互默认回车就好了,我们这里查看public key

```
cat /Users/chihuan/.ssh/id_rsa.pub
```

3.将public key添加到github page项目

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72516d86-924e-44b0-a4a9-3fd58c2e719c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72516d86-924e-44b0-a4a9-3fd58c2e719c/Untitled.png)

4.将private key添加到github hexo项目

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78d8233f-58a0-4f08-8b5e-7422456cd9f0/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78d8233f-58a0-4f08-8b5e-7422456cd9f0/Untitled.png)

### 在hxeo源码项目中配置配置github workflows

```
name: Hexo Auto-Deploy
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    name: Hexo Auto-Deploy by GitHub Actions
    runs-on: ubuntu-latest

    steps:
    - name: 1. git checkout...
      uses: actions/checkout@v1
      
    - name: 2. setup nodejs...
      uses: actions/setup-node@v1
    
    - name: 3. install hexo...
      run: |
        npm install hexo-cli -g
        npm install hexo-deployer-git
        npm install
        
    - name: 4. hexo generate public files...
      run: |
        hexo clean
        hexo g  
    - name: 5. hexo config ...
      env:
          ACTION_DEPLOY_KEY: ${{ secrets.hexo }}
      run: |
          # set up private key for deploy
          mkdir -p ~/.ssh/
          echo "$ACTION_DEPLOY_KEY" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          # set git infomation
          git config --global user.name 'xpfyg'
          git config --global user.email '997052247@qq.com'
          # install dependencies
          npm i -g hexo-cli
          npm i
     
    - name: 6. hexo deploy ...
      run: 
        hexo d
```

### 前提描述

hexo 创建文档后需要将编译后的public目录提交到git线,git page  才能更新，所以有两条代码线，为了减少提交静态代码到git page的操作，通过git action 实现提交hexo代码后自动更新git page的代码

### hexo _config.yml修改配置

```
deploy:
  type: 'git'
  repo: git@github.com:xpfyg/xpfyg.github.io.git
  branch: master
```

### 添加密钥对

1.运行以下终端命令，将电子邮件替换为连接到您的GitHub帐户的电子邮件。

```
ssh-keygen -t rsa -C "997052247@qq.com"
```

2.出现的交互默认回车就好了,我们这里查看public key

```
cat /Users/chihuan/.ssh/id_rsa.pub
```

3.将public key添加到github page项目

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72516d86-924e-44b0-a4a9-3fd58c2e719c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72516d86-924e-44b0-a4a9-3fd58c2e719c/Untitled.png)

4.将private key添加到github hexo项目

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78d8233f-58a0-4f08-8b5e-7422456cd9f0/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78d8233f-58a0-4f08-8b5e-7422456cd9f0/Untitled.png)

### 在hxeo源码项目中配置配置github workflows

```
name: Hexo Auto-Deploy
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    name: Hexo Auto-Deploy by GitHub Actions
    runs-on: ubuntu-latest

    steps:
    - name: 1. git checkout...
      uses: actions/checkout@v1
      
    - name: 2. setup nodejs...
      uses: actions/setup-node@v1
    
    - name: 3. install hexo...
      run: |
        npm install hexo-cli -g
        npm install hexo-deployer-git
        npm install
        
    - name: 4. hexo generate public files...
      run: |
        hexo clean
        hexo g  
    - name: 5. hexo config ...
      env:
          ACTION_DEPLOY_KEY: ${{ secrets.hexo }}
      run: |
          # set up private key for deploy
          mkdir -p ~/.ssh/
          echo "$ACTION_DEPLOY_KEY" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          # set git infomation
          git config --global user.name 'xpfyg'
          git config --global user.email '997052247@qq.com'
          # install dependencies
          npm i -g hexo-cli
          npm i
     
    - name: 6. hexo deploy ...
      run: 
        hexo d
```
