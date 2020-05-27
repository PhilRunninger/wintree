# MinTree

A minimalist version of [NERDTree](https://github.com/scrooloose/nerdtree). How much of NERDTree can I replicate with the fewest lines of code while, at the same time, doing it faster? This project is my answer to that question.

## Prerequisite

MinTree requires Vim version 8.0+, and it must be compiled with the `folding`, `conceal`, and `lambda` features turned on. Make sure you see `+folding`, `+conceal`, and `+lambda` in the output of `:version` or `vim --version`.

## Installation

Use your favorite plugin manager to install this plugin. [vim-pathogen](https://github.com/tpope/vim-pathogen), [Vundle.vim](https://github.com/VundleVim/Vundle.vim), [vim-plug](https://github.com/junegunn/vim-plug), [neobundle.vim](https://github.com/Shougo/neobundle.vim), and [dein.vim](https://github.com/Shougo/dein.vim) are some of the more popular ones. A lengthy discussion of these and other managers can be found on [vi.stackexchange.com](https://vi.stackexchange.com/questions/388/what-is-the-difference-between-the-vim-plugin-managers).

If you have no favorite, or want to manage your plugins without 3rd-party dependencies, I recommend using Vim 8 packages, as described in Greg Hurrell's excellent Youtube video: [Vim screencast #75: Plugin managers](http://img.youtube.com/vi/X2_R3uxDN6g/0.jpg)

## Commands

### `:MinTree [path]`
This command opens a buffer with the name **`=MinTree=`** in the current window, and shows a tree of either the path given or the current working directory.

### `:MinTreeFind [path]`
This command searches the **`=MinTree=`** buffer for the given path. If no path was given, it looks for the current buffer. If not found in the current tree, a new one is created to show the file being sought.

The commands can be assigned to a key, and these assignments are left to the user, so as not to interfere with any existing mappings. For example,

```vim
nnoremap <leader>o :MinTree<CR>
nnoremap <leader>f :MinTreeFind<CR>
```

To split the window first, mappings like these can be used:

```vim
nnoremap <leader>vo :vsplit<Bar>wincmd H<Bar>MinTree<CR>
nnoremap <leader>ho :split<Bar>wincmd J<Bar>MinTree<CR>
```

## Key Bindings

The following, configurable key bindings are used only within the **`=MinTree=`** buffer. The lists below show the default key bindings, a description of the action each key performs, and the corresponding global variable.

#### Opening/Closing Buffers
- **`o`** ⮕ Open the selected file in the current window, or expand or collapse the directory. (`g:MinTreeOpen`)
- **`O`** ⮕ Fully expand the selected directory. (`g:MinTreeOpenRecursively`)
- **`s`** ⮕ Split the window horizontally, and open the selected file there. (`g:MinTreeOpenSplit`)
- **`v`** ⮕ Split the window vertically, and open the selected file there. (`g:MinTreeOpenVSplit`)
- **`t`** ⮕ Open the selected file in a new tab. (`g:MinTreeOpenTab`)
- **`w`** ⮕ Close the buffer associated with the selected node. (`g:MinTreeWipeout`)
#### Navigating the Tree
- **`p`** ⮕ Navigate quickly to the closest parent directory. (`g:MinTreeGoToParent`)
- **`J`** ⮕ Navigate quickly to the last sibling file or directory. (`g:MinTreeLastSibling`)
- **`K`** ⮕ Navigate quickly to the first sibling file or directory. (`g:MinTreeFirstSibling`)
- **`<C-J>`** ⮕ Navigate quickly to the next sibling file or directory. (`g:MinTreeNextSibling`)
- **`<C-K>`** ⮕ Navigate quickly to the previous sibling file or directory. (`g:MinTreePrevSibling`)
#### Updating the Tree
- **`u`** ⮕ Change the root of the tree to the parent directory of the current root. (`g:MinTreeSetRootUp`)
- **`C`** ⮕ Change the root of the tree to the directory under the cursor. (`g:MinTreeSetRoot`)
- **`x`** ⮕ Collapse the directory containing the current file or directory. (`g:MinTreeCloseParent`)
- **`r`** ⮕ Refresh the selected directory or the directory containing the selected file. (`g:MinTreeRefresh`)
- **`R`** ⮕ Refresh the whole tree. (`g:MinTreeRefreshRoot`)
- **`I`** ⮕ Toggles hidden files, those starting with a period, or marked hidden in Windows. (`g:MinTreeToggleHidden`)
#### Bookmarks
- **`m`** ⮕ Creates a single-letter bookmark for the current node. (`g:MinTreeCreateMark`)
- **`'`** ⮕ Displays all bookmarks, and opens the one selected. (`g:MinTreeGotoMark`)
- **`dm`** ⮕ Displays all bookmarks, and deletes the ones selected. This is the same key used for creating bookmarks, but prefixed with a `d`. (`g:MinTreeCreateMark`)
#### Miscellaneous
- **`q`** ⮕ Exit the MinTree, and return to the previous buffer. (`g:MinTreeExit`)
- **`?`** ⮕ Display short descriptions of these commands.

## Settings

* The following variables define the OS commands that gather files and directories. If necessary, you can customize them for your unique situation.

    Variable | Default
    --- | ---
    **`g:MinTreeDirAll`**<br>returns all files/dirs in the `%s` directory. | Windows: `dir /b %s`<br>others: `ls -A %s \| sort -f`
    **`g:MinTreeDirNoHidden`**<br>returns all non hidden files/dirs in the `%s` directory. | Windows: `dir /b /a:-h %s \| findstr -v "^\."`<br>others: `ls %s \| sort -f`
    **`g:MinTreeShowHidden`**<br>sets which of the above two commands to use by default. | 0

* The characters used to indicate whether a directory is collapsed or expanded can be customized with these two variables

    Variable | Default
    --- | ---
    **`g:MinTreeExpanded`**<br>Character used to indicate a directory's contents are being shown. | `▾`
    **`g:MinTreeCollapsed`**<br>Character used to indicate a directory's contents are hidden or not yet retrieved. | `▸`

* To change the indentation level, change the value of **`g:MinTreeIndentSize`**. It is the number of spaces to use for each level of indentation, and its default value is `2`.
