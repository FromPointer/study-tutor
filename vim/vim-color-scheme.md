## This is file about VIM COLOR SCHEME and config.

***
###VIM Color Scheme Website
[VIM Script Main](http://www.vim.org/scripts/script_search_results.php?keywords=&script_type=color+scheme&order_by=creation_date&direction=descending&search=search)
[VIM Color Sets](https://code.google.com/p/vimcolorschemetest/)


***
###VIM Color Config Steps
####1. 



***
###VIM Color Plugin (csExplorer.vim)
This is a vim-color plugin (Color Scheme Explorer).
Color Scheme Explorer display a list of all available color schemes you have installed on your computer. Once opened, you are able to scroll through the list and select the color scheme of your choice.



***
####VIM ColorScheme Procedure:

#####Vim Color Scheme File
Default Vim Color Scheme file is in the `color` of vim installed directory
######Eg:
    In Mac, default color directory:
    /usr/local/share/vim/vim74/colors

    In CentOS, default color directory:
    /usr/share/vim/vim74/colors
    
__Color Scheme Download Address:__
[Color Scheme Explorer](http://www.vim.org/scripts/script.php?script_id=1298)
[Github csExplorer](https://github.com/jdevera/vim-cs-explorer)
[VIM Color Scheme From Google](http://vimcolorschemetest.googlecode.com/svn/colors/)
[vimcolorscheme](https://code.google.com/p/vimcolorschemetest/)

#####Add Color Scheme
Download Color Scheme file from aboving website, then add this file to `Color Scheme Directory` directory.


###Color Scheme Selection

####Direct Choose Color-Scheme
In `~/.vimrc` file, add following line:
    colorscheme [color-scheme-name]
    


####Using plugin `csExplorer` management
#####Intalling plugin
1. Installing using pathogen 
    cd ~.vim
    git clone https://github.com/jdevera/vim-cs-explorer bundle/csExplorer

2. direct installing plugin
Download [`csExplorer`](http://www.vim.org/scripts/script.php?script_id=1298),
then Extract to `.vim` directory.



####Usage
In vim edit mode, using default the command to invoke the Color Scheme Explorer
    :ColorSchemeExplorer




***
###Reference
[SOLARIZED Main Page](http://ethanschoonover.com/solarized)

[Vim Plugin Installing](http://blog.csdn.net/namecyf/article/details/7787479)


