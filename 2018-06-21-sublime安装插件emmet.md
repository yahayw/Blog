# 下载安装sublime软件，sublime软件的一个插件--emmet好用，接下来安装步骤走起。
## 1.通过快捷键ctrl+` 或者通过菜单栏中的View->Show Console打开控制台
### 粘贴如下代码（sublime text 3）：
> import  urllib.request,os;pf='Package Control.sublime-package';ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),'wb').write(urllib.request.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read())
### 2.ctrl+shift+p快捷键-->Package Control: Install Package-->emmet-->回车安装此emmet插件
