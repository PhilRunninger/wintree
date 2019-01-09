# MinTree

A minimalist version of [NERDTree](https://github.com/scrooloose/nerdtree). How much of NERDTree can I replicate with the fewest lines of code while, at the same time, doing it faster? This project is my answer to that question.

## Prerequisite

MinTree uses the `folding` and `conceal` features of Vim. It should run on Vim version 7.3+, as long as it is compiled with those features enabled. Make sure you see `+folding` and `+conceal` in the output of `:version`.

## Installation

Use your favorite plugin manager to install this plugin. My personal favorite is [vim-plug](https://github.com/junegunn/vim-plug). In your **`.vimrc`**, add the following line.
```vim
Plug 'git@github.com:PhilRunninger/mintree.git'
```

[Vundle](https://github.com/VundleVim/Vundle.vim), [pathogen](https://github.com/tpope/vim-pathogen), and others should also work as easily. Just follow the convention set up by the plugin manager of your choice.

## Commands

### **`:MinTree [path]`**
This command opens a buffer with the name **`=MinTree=`** in the current window, and shows a tree of either the path given or the current working directory.

### **`:MinTreeFind [path]`**
This command searches the **`=MinTree=`** buffer for the given path. If no path was given, it looks for the current buffer. If not found in the current tree, a new one is created to show the file being sought.

The commands can be assigned to a key, and these assignments are left to the user, so as not to interfere with any existing mappings. For example,
```
nnoremap <leader>o :MinTree<CR>
nnoremap <leader>f :MinTreeFind<CR>
```

## Key Mappings

The following key mappings are used only within the **`=MinTree=`** buffer. They are configurable by setting the corresponding global variables.

Default Key | Variable                   | Function
---         | ---                        | ---
**`o`**     | `g:MinTreeOpen`            | Open the selected file in the current window, or expand/close the directory.
**`O`**     | `g:MinTreeOpenRecursively` | Fully expand the tree under the cursor.
**`s`**     | `g:MinTreeOpenSplit`       | Split the window horizontally, and open the selected file there.
**`v`**     | `g:MinTreeOpenVSplit`      | Split the window vertically, and open the selected file there.
**`t`**     | `g:MinTreeOpenTab`         | Open the selected file in a new tab.
**`p`**     | `g:MinTreeGoToParent`      | Navigate quickly to the next closest parent folder.
**`u`**     | `g:MinTreeSetRootUp`       | Change the root of the tree to the parent directory of the current root.
**`C`**     | `g:MinTreeSetRoot`         | Change the root of the tree to the directory under the cursor.
**`x`**     | `g:MinTreeCloseParent`     | Close the directory containing the current file or directory.
**`r`**     | `g:MinTreeRefresh`         | Refresh the directory under the cursor, or the directory containing the file under the cursor.
**`R`**     | `g:MinTreeRefreshRoot`     | Refresh the whole tree.
**`I`**     | `g:MinTreeToggleHidden`    | Toggles the display of hidden files, those starting with a period, or marked hidden in Windows.
**`q`**     | `g:MinTreeExit`            | Exit the MinTree, and return to the previous buffer.

## Settings

The following settings can be used to customize the commands that gather files and directories for your unique situation.

Variable | Default
--- | ---
**`g:MinTreeDirAll`**<br>returns all files/dirs in the `%s` folder. | Windows: `dir /b %s`<br>others: `ls -A %s \| sort -f`
**`g:MinTreeDirNoHidden`**<br>returns all non hidden files/dirs in the `%s` folder. | Windows: `dir /b /a:-h %s \| findstr -v "^\."`<br>others: `ls %s \| sort -f`
**`g:MinTreeShowHidden`**<br>sets which of the above two commands to use by default. | 0
