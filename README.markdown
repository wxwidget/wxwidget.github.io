## 我的个人日志系统


## 准备
注意：
这里需要两个branch，
* master存放生成好的文件。
* source存放修改后的[octopress](http://github.com/imathis/octopress)源代码

##安装
1. 安装git
2. rvm , ruby (1.9.3) 和 (bundle)
3. clone 代码:

    ```bash
    $ git clone https://github.com/imathis/octopress.git myblog  
    或者
    $ git clone -b source https://github.com/wxwidget/wxwidget.github.io.git myblog
    ```
4. 安装依赖的ruby库, gem->package management, bundle->dependency management:

    ```bash
    $ cd myblog
    $ gem install bundle 
    $ bundle install 
    ```
5. Install the default theme:

    ```bash
    $ rake install
    ```
6. 设置github

    ```bash
    $ rake setup_github_pages
    $ rake generate
    $ rake deploy
    ```
7. 启动预览

    ```bash
    $ rake preview
    ```
8. 写文章 

    ```bash
    $ rake 'new_post["title"]'
    ```
9. source提交到branch

    ```bash
    $ git add .
    $ git commit -m 'your message' 
    $ git push origin source
    ```
10. 生成导航page

    ```
    $ rake new_page["new_pages"]
    $ vi /source/_includes/custom/navigation.html
   ```
## Powerby octopress

Check out [Octopress.org](http://octopress.org/docs) for guides and documentation.
