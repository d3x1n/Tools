## VS Code使用攻略

### 目录

+ #### [基础](#1)

+ #### [使用技巧](#2)
    + ##### [同步功能](#21)
    + ##### [Remote - SSH插件配置免密访问服务器](#22)
    + ##### [python相关常用功能](#23)
    + ##### [LaTex](#24)
    + ##### [编辑器颜色与代码高亮](#25)

+ #### [其他可配置功能](#3)

+ #### [setting.json配置参考](#4)

### <a id="1">1. 基础</a>

[下载]https://code.visualstudio.com/

下载时注意勾选右键菜单添加通过Code打开的选项，默认是不勾选的

**插件推荐**
- Chinese (Simplified) Language Pack for Visual Studio Code : 中文语言包
- Python
- Remote - SSH : SSH连接服务器插件
- Bracket Pair Colorizer 2 : 括号匹配高亮指示
- LaTex Workshop : 使用VS Code写LaTex
- LeetCode
- select highlight in minimap : minimap代码高亮
- highlight-icemode : 选中代码高亮
- Markdown All in One : Markdown支持

### <a id="2">2. 使用技巧</a>
+ #### <a id="21">同步功能</a>

设置中可以开启登录同步功能，通过在不同的电脑登录MicroSoft/Github账号同步VS Code的大部分配置，简化重装软件后的配置过程

+ #### <a id="22">Remote - SSH插件配置免密访问服务器</a>
1. 本地win+R进入命令提示符界面
```
ssh-keygen -t rsa -b 4096 #生成RSA格式公钥
# 全部默认设置，不要设置密语，生成私钥名称id_rsa，公钥名称id_rsa.pub
# 记住显示的文件保存路径
```
2. 将公钥文件id_rsa.pub拷贝至服务器端
3. 将公钥写入authorized_keys 文件
```
touch ~/.ssh/hah/authorized_keys  #如果没有则需要新建
cat id_rsa.pub >> authorized_keys 
```
此时可以从本地免密访问服务器,访问方式如下
```
ssh $username@$server_ip # ssh xxx@10.12.13.235
```
4. 配置简称
在本地个人目录下的.ssh文件夹找到config文件,User填写服务器端用户名
```
Host server231
    HostName 10.12.13.231
    User xxx
    StrictHostKeyChecking no
Host server235
    HostName 10.12.13.235
    User xxx
    StrictHostKeyChecking no
```
此时可以从本地通过简称访问服务器，如
```
ssh server231
```
5. VS Code编辑器中远程连接
在左侧图标中选择远程资源管理器，可以进行服务器的访问操作。菜单栏中的终端选项可以新建终端。

+ #### <a id="23">python相关常用功能</a>

    + 通用的调试，代码补全，代码纠错，快捷切换环境等功能,可以[配置禁用部分flake8报错信息](#flake8)
    + 右键格式化美化代码
    + 在打开的文件夹中同时选中两个代码文件，右键可以将已选项进行比较
    + shift+enter 开启交互式命令环境

+ #### <a id="24">LaTex</a>


    + [下载TexLive](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)

    + [setting.json配置如下](#latex)

+ #### <a id="25">编辑器颜色与代码高亮</a>

    + 插件商城中下载
    + 通过CSS代码自定义编译器，[个人配置如下](#color)



### <a id="3">3. 其他可配置功能</a>

- Git管理 : 在GUI中进行Git代码管理
- [C/C++](https://code.visualstudio.com/docs/cpp/config-mingw)
- 插件市场中各种Theme和icon图标插件

### <a id="4">4. setting.json配置参考</a>

+ #### <a id="flake8">配置禁用部分flake8报错信息</a>
```json
    "python.linting.flake8Args": [
        "--max-line-length=1000",
        "--extend-ignore=E231,E203,E117,E302,E225,E228,W291,E305,W191,W292,W391"
    ],
```

+ #### <a id="latex">latex配置</a>
```json
"latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        },
        {
            "name": "pdflatex -> bibtex",
            "tools": [
                "pdflatex",
                "bibtex"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "xelatex -> bibtex -> xelatex*2",
            "tools": [
            "xelatex",
            "bibtex",
            "xelatex",
            "xelatex"
            ]
        }
    ],
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk"
    ],
```
+ #### <a id="color">编辑器颜色与代码高亮</a>
```json
    "editor.tokenColorCustomizations": {
        "[Default Dark+]": {
            
            "textMateRules": [

                {
                    "name": "comment",
                    "scope":"comment",
                    "settings": {
                        "foreground": "#c6f18eca",
                        "fontStyle":"italic bold"
                    }
                },
                {
                    "name": "python docstring",
                    "scope":[
                        "string.quoted.docstring.multi.python",
                        "string.quoted.multi.python",
                    ],
                    "settings": {
                        "foreground": "#bdb2e2",
                    }
                },
                {
                    "name": "python constant number",
                    "scope":[
                        "constant.numeric.dec.python",
                        "constant.numeric.float.python",

                    ],
                    "settings": {
                        "foreground": "#74e6ade5",
                    }
                },
                {
                    "name": "python constant",
                    "scope":[
                        "constant.other.caps.python",
                    ],
                    "settings": {
                        "foreground": "#62a6f3",
                    }
                },
            ]
        }
    },
```








