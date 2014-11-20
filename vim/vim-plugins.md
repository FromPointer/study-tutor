#Vim插件简单介绍

## Pathogen
pathogen为管理插件的插件，类似的还有vundle。在 Pathogen 之前，安装插件就是把插件文件放在.vim目录下，所有的插件都混在一起，不便于管理。

####通过pathogen，可以将不同的插件放到不同的目录里，比如：

    ~  tree .vim/bundle -L 2
    .vim/bundle
        ├── SingleCompile
        │   ├── COPYING
        │   ├── README.rst
        │   ├── autoload
        │   ├── doc
        │   ├── mkzip.sh
        │   └── plugin

####pathogen的安装十分简单，只需要将pathogen.vim clone到.vim/autoload/pathogen.vim目录，然后在`.vimrc`配置文件加下面内容即可：

    runtime autoload/pathogen.vim
    execute pathogen#infect()

#####或者可以将pathogen放在其他地方，然后在.vimrc加上如下内容：

    source ~/src/vim/bundle/vim-pathogen/autoload/pathogen.vim
    execute pathogen#infect()



## Nerdtree

Nerdtree用来浏览文件系统并打开文件或目录。
nerdtree提供如下功能及特性：

1. 以继承树的形式显示文件和目录
2. 对如下类型的文件进行不同的高亮显：文件、目录、sym-links、快捷方式、只读文件、可执行文件。
3. 提供许多映射来控制树状结构
4. 对树状结构内容的过滤（可在运行时切换），如自定义文件过滤器阻止某些文件（比如vim备份文件等）的显示、可选是否显示隐藏文件、可选不显示文件只显示目录
5. 可以自定义Nerd窗口的位置和大小，自定义结点排序方式
6. 可以将文件和目录添加到收藏夹，可以用书签标记某些文件或者目录


## Xptemplate
安装完成后:Helptags生成帮助文档，然后:h xpt查看帮助文档。

要想看当前文件类型支持的代码片段，可以在insert模式下键入`<C-r><C-r><C-\>`。
insert模式下输入片段的名字，然后`<C-\>`即可插入代码，然后可以用`TAB、Shift Tab`前后更改高亮显示的内容。

## YouCompleteMe
YCM是一个比较新Vim代码补全插件，默认为程序语言提供基于标识符的补全。它会收集当前文件、tags文件以及其他访问过的文件中的标识符，当输入时，会自动显示匹配的标识符。YCM不需要TAB即可呼出匹配的标识符，可以一边输入一边参考YCM呼出的菜单。YCM的强大之处还在于，它的匹配并不是前缀匹配，而是子字符串匹配，也就是说如果输入abc，那么标识符中的xaybgc也会匹配，而不只是abc...。

    Installing refer to [YouCompleteMe Main Page](http://valloric.github.io/YouCompleteMe/)



***
From: [git plugins config](http://xuelangzf.github.io/06-11-2013/vim_plugins.html)



