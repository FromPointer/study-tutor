# Use VIM as Xcode alternative

##1. Installing Packages
    In order to get Vim to behave nice with XCode, a couple of plugins are necessary. In order to install them, I’d recommend using a package manager like Pathogen or Vundle. I’m using Vundle. This means that whenever you see something like “Bundle ‘name/plugin’” in my Vim configuration, it is a Vundle command that will look up the Vim plugin on Github, download it, and include it - all in one step.


##2. Clang
Using [Homebrew](http://brew.sh/) to install clang
    brew install --HEAD llvm --with-clang


##[Clang Complete](https://github.com/Rip-Rip/clang_complete) Vim plugin 
Using Pathogen to install clang_complete vim plugin
    You can [download it here](https://github.com/Rip-Rip/clang_complete).
Below is configuration to make it work.
    " Tell Vundle to download & import the clang complete plugin
    Bundle 'Rip-Rip/clang_complete'

    " Disable auto completion, always <c-x> <c-o> to complete
    let g:clang_complete_auto = 0 
    let g:clang_use_library = 1
    let g:clang_periodic_quickfix = 0
    let g:clang_close_preview = 1

    " For Objective-C, this needs to be active, otherwise multi-parameter methods won't be completed correctly
    let g:clang_snippets = 1

    " Snipmate does not work anymore, ultisnips is the recommended plugin
    let g:clang_snippets_engine = 'ultisnips'

    " This might change depending on your installation
    let g:clang_exec = '/usr/local/bin/clang'
    let g:clang_library_path = '/usr/local/lib/libclang.dylib'


###Cmd Behaviour
    <c-x> <c-o> Show list of completions


##Ultisnips
For the actual completion, Clang Complete has its own code but can also work with different completion plugins. I found the Clang Complete solution to not work very well, so I tested the others. Ultisnips comes closest to the XCode experience. It also includes a set of readymade snippets for common Objective-C patterns.

###So next up you need to [install ultisnips](https://github.com/SirVer/ultisnips):

    Bundle 'guns/ultisnips'

In XCode, when you want to switch between several parameters on a selector (doSomething:<> toObject:<> withObject:<>) you can just hit or +. This does not work with ultisnips, instead you have to type or .

###Cmd Behaviour
    <c-j>   Go to next parameter in completion
    <c-k>   Go to previous parameter
###Snippet Behaviour
    cl<tab> Define Class
    sel<tab>    @selector(example:)
    log<tab>    NSLog(…)
    format<tab> NSString stringWithForma


##Indentation
Vim’s default Objective-C indent is not very functional. 
Thankfully, Björn Winckler, a main contributor to MacVim, [released a very good plugin for this](https://github.com/b4winckler/vim-objc), 
that fixes all the issues I had:
    Bundle "b4winckler/vim-objc"


##Switching Header Files
Another feature of XCode that I could not live without is the easy way to switch between header and implementation. [Vim-iOS](https://github.com/eraserhd/vim-ios) adds commands for this. With :A you can switch to the alternate file. In addition to that it also offers :XBuild for building your project and :Xinstall for installing it on a device.
    Bundle 'eraserhd/vim-ios.git'

###Cmd Behaviour
    :A  Switch to alternate file
    :XBuild Compile Project
    :Xinstall   Install on device
    
From: [vim objective-c tool config](http://appventure.me/2013/01/29/use-vim-as-xcode-alternative-ios-mac-cocoa/)
