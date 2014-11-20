#YouCompleteMe's Installing

##1. Goto YouCompleteMe
    Entering into [YouCompleteMe](https://github.com/Valloric/YouCompleteMe)

##2. Download YouComplete

###2.1 Using **pathogen** Tool
#### About **pathogen** installing, refer to [pathogen Main page](https://github.com/vim-scripts/pathogen.vim)

    cd .vim
    git submodule add https://github.com/Valloric/YouCompleteMe bundle/YouCompleteMe
    git submodule update --init --recursive


###2.2 Using Vundle
#### About **Vundle** installing, refer to [Vundle Main page](https://github.com/gmarik/Vundle.vim)

    cd ~/.vim
    git clone https://github.com/Valloric/YouCompleteMe bundle/Valloric/YouCompleteMe

#####Add **Plugin Descriptor** to .vimrc file
    Plugin 'bundle/Valloric/YouCompleteMe'(plugin directory)
    Plugin syntax: supporting local direcotry, git-URL, rtp etc.

#####In vim editting, installing plugin
    :PluginInstall

If you don't install YCM with Vundle, make sure you have run `git submodule update --init --recursive` after checking out the YCM repository 
    
###2.3 Cloning and Building-->Mannually Installing
    
    cd .vim
    git clone https://github.com/Valloric/YouCompleteMe bundle/YouCompleteMe
    git submodule update --init --recursive
    cd bundle/YouCompleteMe
    ./install.sh --clang-completer --system-clang --system-boost
    




***
From: [git YouCompleteMe](https://github.com/Valloric/YouCompleteMe)
    
    
