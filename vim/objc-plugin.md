#Objective-c plugin usage in VIM

##Build Objective-c
Installing [xcodebuild-rb](https://github.com/lukeredpath/xcodebuild-rb) gem
###In .vimrc:
    nmap <leader>x :!rake xcode_build<CR>
    nmap <leader>cl :!rake clang_db<CR>


####Jump in function
    CTRL-]
####Check syntax
    g:ClangUpdateQuickFix()



##Running project in simulator and Unit Testing
With my Rake task I was able to compile my project, next step was to run it with iOS simulator. I already knew a great solution for quite a while from my previous experiments with
[Jenkins](http://jenkins-ci.org/)

###Installing [ios-sim](https://github.com/phonegap/ios-sim)

After integrating iOS simulator into Vim, I proceeded with unit testing.
###Installing unitTest: Guard and guard-ocunit
I always wanted to get a [Guard](https://github.com/guard/guard) based approach with Xcode, running single test from Xcode was a problem, so I created myself a plugin for Guard [guard-ocunit](https://github.com/ap4y/guard-ocunit).



##Debugging
I found a great vim-lldb plugin (by Daniel Malea) inside llvm-project sources (svn, unofficial git mirror). It uses [lldb](http://lldb.llvm.org/python-reference.html) Python API and implements UI via vimscript. Unfortunately, attach command was not a part of the plugin,
so I decided to add it. It took me a while to study sources and API documentation, 
but I was able to produce working solution in a couple hours.
