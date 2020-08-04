## Git基础配置
+ 签名配置
  + 系统级别：

  ```bash
  git config --global user.name "Zoran"
  git config --global user.email 1195815445@qq.com
  ```
  
  + 项目级别/仓库级别：仅在当前本地库范围内有效
  
  ```bash
   git config user.name tom_pro  
   git config user.email goodMorning_pro@atguigu.com  
   信息保存位置：./.git/config 文件
  ```
  
  > 上述二者的优先级别为就近原则，项目配置优先
  
  

+ 基本操作

  <img src="./image-20200804142947147.png" alt="image-20200804142947147" style="zoom: 33%;" />

## 本地库

```bash
git init 		#初始化本地仓库
git status 	#查看工作区、暂存区状态
git commit -m "commit message" [file name] #将暂存区的内容提交到本地库
git commit -a   #修改文件后直接提交不用git add
```

`git log`:

<img src="./image-20200804145715802.png" alt="image-20200804145715802" style="zoom:75%;" />

`git log --pretty=oneline`

<img src="./image-20200804150049555.png" alt="image-20200804150049555" style="zoom:75%;" />

`git log --oneline`

<img src="./image-20200804150211550.png" alt="image-20200804150211550" style="zoom:75%;" />

`git reflog`

<img src="./image-20200804150348168.png" alt="image-20200804150348168" style="zoom:75%;" />