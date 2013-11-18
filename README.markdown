## 我的个人日志系统


## 准备
注意：
这里需要两个branch，
* master存放生成好的文件。
* source存放修改后的octopress源代码

##安装
1. 安装git
2. rvm , ruby (1.9.3) 和 (bundle)
3. clone 代码
'''bash
git clone https://github.com/imathis/octopress.git myblog

or

git clone -b source https://github.com/wxwidget/wxwidget.github.io.git myblog

'''

4. 安装依赖的ruby库, gem->package management, bundle->dependency management
'''bash
cd myblog
gem install bundle 
bundle install 
'''

5.Install the default theme:
'''bash
rake install
'''

6. 设置github
'''bash
rake setup_github_pages
rake generate
rake deploy

'''

8. 启动预览
'''bash
rake preview
'''


9.写文章 
''bash
rake 'new_post["title"]'
'''

10. source提交到branch
git add .
git commit -m 'your message' 
git push origin source

## Powerby octopress

Check out [Octopress.org](http://octopress.org/docs) for guides and documentation.
