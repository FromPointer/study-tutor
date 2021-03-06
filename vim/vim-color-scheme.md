## This is file about VIM COLOR SCHEME and config.

***
###VIM Color Scheme References
__[VIM Script Main](http://www.vim.org/scripts/script_search_results.php?keywords=&script_type=color+scheme&order_by=creation_date&direction=descending&search=search)__       
__[VIM Color Sets Google](https://code.google.com/p/vimcolorschemetest/)__


***
##VIM Color Scheme Config Steps

***
###1. VIM Color Scheme Management Plugin (csExplorer.vim)
This is a vim-color plugin : [Color Scheme Explorer](http://www.vim.org/scripts/script.php?script_id=1298).
Color Scheme Explorer display a list of all available color schemes you have installed on your computer. Once opened, you are able to scroll through the list and select the color scheme of your choice.

####__Installing plugin__
######*. Installing using pathogen
    cd ~.vim
    git clone https://github.com/jdevera/vim-cs-explorer bundle/csExplorer

__[*Tips]__ If didn't install Pathogen, refer to [Pathogen's Installing](https://github.com/FromPointer/.vim-tutor/wiki/pathogen-install-plugins)

######*. Direct installing plugin
Download [`csExplorer`](http://www.vim.org/scripts/script.php?script_id=1298),
then Extract to `.vim` directory.



***
###2. Vim Color Scheme File
Default Vim Color Scheme file is in the `colors` of vim installed directory
Eg:
######In Mac, default color directory:    
    /usr/local/share/vim/vim74/colors    

######In CentOS, default color directory:
    /usr/share/vim/vim74/colors
    
__VIM Color Scheme File Download Address:__    
[Color Scheme Explorer](http://www.vim.org/scripts/script.php?script_id=1298)    
[Github csExplorer](https://github.com/jdevera/vim-cs-explorer)    
[VIM Color Scheme From Google](http://vimcolorschemetest.googlecode.com/svn/colors/)    
[vimcolorscheme](https://code.google.com/p/vimcolorschemetest/)    
[vimcolors.com](http://vimcolors.com/)


***
###2. Add Color Scheme File
Download `Color Scheme File` from aboving website, then add the file to `Color Scheme Directory`.

You can put `the Color-Scheme-File` to default's system directory, or put into `~/.vim/colors` directory.


***
###3. Color Scheme Settings

####*. Direct Choose Color-Scheme
######In `~/.vimrc` file, add following line:
    colorscheme [color-scheme-name]
    
    
####*. Using plugin `csExplorer` setting
######In vim edit mode, using 'following's command' to invoke the Color Scheme Explorer
    :ColorSchemeExplorer
    then select scheme you liked, __Return__

__[*Tips]__ Using plugin `csExplorer`, after selecting color scheme, `close vim`, the `color sheme` miss; If you like the `color scheme`, you need to modify `colorscheme` to "Color Name" you liked in `.vimrc` file. 



***
###Reference
[SOLARIZED Main Page](http://ethanschoonover.com/solarized)

[Vim Plugin Installing](http://blog.csdn.net/namecyf/article/details/7787479)


