---
author: "韩立"
title: "配置日记"
date: "2022-09-21"
description: "第二次操作失误:cold_sweat:重装了~"
ShowBreadCrumbs: false
tags: ["configuration"]
---

第一次某个电脑清理软件给我 WSL2 全删了，第二次 nt 的去删掉了 ubuntu20 内置的 python3.8(/usr/bin/python3.8、/usr/local/lib/python3.8) 导致包管理错误。[Broken python dependencies after trying to re-install](https://askubuntu.com/questions/1065556/broken-python-dependencies-after-trying-to-re-install)

## 各语言 Formatter 和 Linter

Formatter

- Python -autopep8 / Black
- Java - Google Java Format
- C++ - Clang-Format
- JavaScript/TypeScript - Prettier
- Ruby - RuboCop
- Go - gofmt
- Rust - Rustfmt

Linter

- Python - pylint/ruff
- Java - checkstyle / SpotBugs
- C++ - clang-tidy (clangd) / IntelliSense in Visual Studio
- JavaScript/TypeScript - ESLint
- Ruby - RuboCop
- Go - Golangci-lint
- Rust - Clippy

## 主题配色

- Atom One Light Theme
- Atom One Dark Theme
- Penumbra 有明暗两个主题，据说是通过数学计算得到的、最有利于感知的配色方案。
- Dracula

## 图床

- https://github.com/XmchxUp/cloudimg
  [PicX](https://picx.xpoet.cn/#/upload)

## Java

多版本切换试例
~/.bashrc

```sh
JAVA_HOME_8=/Library/Java/JavaVirtualMachines/jdk1.8.0_192.jdk/Contents/Home
JAVA_HOME_11=/Users/Kevin/development/tools/jdk-11.0.16.1.jdk/Contents/Home
JAVA_HOME_17=/Users/Kevin/development/tools/jdk-17.0.4.1.jdk/Contents/Home
JRE_HOME=$JAVA_HOME/jre
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.
export JAVA_HOME=$JAVA_HOME_8
export JRE_HOME
export PATH
export CLASSPATH

alias jdk8="export JAVA_HOME=$JAVA_HOME_8"
alias jdk11="export JAVA_HOME=$JAVA_HOME_11"
alias jdk17="export JAVA_HOME=$JAVA_HOME_17"
```

source ~/.bashrc

![image](https://cdn.jsdelivr.net/gh/XmchxUp/cloudimg@master/img/image.4bvku01jp2g0.webp)

## Python

设置默认使用 python3

```sh
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.10 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 1
```

- 安装可执行文件使用[pix](https://github.com/pypa/pipx)
- 项目开发不同版本 Python 使用 [pyenv](https://github.com/pyenv/pyenv)
- 项目依赖管理使用 [PDM](https://github.com/pdm-project/pdm)

## Node.js

- 版本管理使用[NVM](https://github.com/nvm-sh/nvm)
- 依赖管理使用[PNpm](https://pnpm.io/)

## 设置代理脚本

proxy.sh

```bash
#!/bin/bash
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
export ALL_PROXY="http://$host_ip:7980"
```

source proxy

## NvChad

> [安装](https://nvchad.com/quickstart/install#pre-requisites)

- [Install a Nerd Font](https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup#install-a-nerd-font)
- [Install Nvim](https://github.com/neovim/neovim/wiki/Installing-Neovim)
- https://github.com/craftzdog/dotfiles-public

## Zsh && Oh My Zsh

> [安装](https://zhuanlan.zhihu.com/p/58073103) [插件](https://zhuanlan.zhihu.com/p/61447507)

```sh
plugins=(git zsh-autosuggestions zsh-syntax-highlighting sudo wakatime zsh-vi-mode)
```

## Git

```sh
git config --global user.name "Ultraman"
git config --global user.email  "1394466835@qq.com"

```

## Windows + WSL2(ubuntu)

### 设置 root 用户的密码

管理员模式打开 powershell, 改变 ubuntu 默认切换的用户 ubuntu2004.exe config --default-user root(这里没用管理员模式又 gg 了直接打不开 ubuntu 了), 关闭 wsl --shutdown 再打开 ubuntu 修改密码 passwd。最后在改回之前的默认用户 ubuntu2204.exe config --default-user tesla。

### 图形化配置~~无缝衔接

> [参考 1](https://zhuanlan.zhihu.com/p/146146238)  
> [参考 2](https://github.com/davidbombal/wsl2/blob/main/ubuntu_gui_youtube)
> 建议使用 Windows X Lanuch(避免 qemu 的坑)

#### 安装 VcXsrc

> [下载](https://sourceforge.net/projects/vcxsrv/)

multiple windows 可以无缝连续直接在 terminal 里用

如果连接不行可以在配置选项时另-ac 参数[see](https://www.bilibili.com/read/cv11143517)

#### 配置与启动 xfce4

```bash
sudo apt install -y xfce4
 # 导出
$ vim ~/.bashrc
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0
```

![image](https://xmchxup.github.io/cloudimg/20220921/image.3demx18juhy0.webp)

## Jetbrains ideavim

```ideavim
let mapleader=" "

""" Common settings -------------------------
set showmode
set so=5
set incsearch
set nu


"" -- Suggested options --
" Show a few lines of context around the cursor. Note that this makes the
" text scroll if you mouse-click near the start or end of the window.
set scrolloff=5

" Do incremental searching.
set incsearch

" Don't use Ex mode, use Q for formatting.
map Q gq

" --- Enable IdeaVim plugins https://jb.gg/ideavim-plugins

" Highlight copied text
Plug 'machakann/vim-highlightedyank'
" Commentary plugin
Plug 'tpope/vim-commentary'



""" Idea specific settings ------------------
set ideajoin
set ideastatusicon=gray
set idearefactormode=keep


""" Mappings --------------------------------
map <leader>r <Action>(RenameElement)

" inoremap jk <Esc>
inoremap kj <Esc>

nnoremap <Tab> gt
nnoremap <S-Tab> gT

nnoremap <Leader>o :action RecentProjectListGroup<CR>

nnoremap K :action QuickJavaDoc<CR>
nnoremap <C-q> :action ParameterInfo<CR>
nnoremap ca :action ShowIntentionActions<CR>

nnoremap <D-C-F> :action ReformatCode<CR>
<!-- windows -->
<!-- nnoremap <C-A-F> :action ReformatCode<CR> -->


nnoremap gb :action LastEditLocation<CR>
nnoremap gi :action GotoImplementation<CR>
nnoremap gm :action GotoSymbol<CR>
nnoremap gh :action Back<CR>
nnoremap gl :action Forward<CR>

nnoremap ga :<C-u>action GotoAction<CR>
nnoremap gc :<C-u>action GotoClass<CR>
nnoremap gd :<C-u>action GotoDeclaration<CR>
nnoremap gs :<C-u>action GotoSuperMethod<CR>
nnoremap gf :<C-u>action GotoFile<CR>
nnoremap gu :<C-u>action ShowUsages<CR>
nnoremap gt :<C-u>action GotoTest<CR>
nnoremap gp :<C-u>action FindInPath<CR>
nnoremap gr :<C-u>action RecentFiles<CR>

nnoremap ]d :action GotoNextError<CR>
nnoremap [d :action GotoPreviousError<CR>

nnoremap u :undo<CR>
nnoremap U :redo<CR>
nnoremap vs :vsplit<CR>
nnoremap sp :split<CR>
nnoremap X :noh<CR>


nnoremap ta :action Annotate<cr>
nnoremap tb :action ToggleLineBreakpoint<cr>
nnoremap tm :action ToggleBookmark<cr>
nnoremap tp :action ActivateProjectToolWindow<CR>


nnoremap <Leader>\ <C-W>v
nnoremap <Leader>- <C-W>s
nnoremap <C-h> <C-W>h
nnoremap <C-l> <C-W>l
nnoremap <C-j> <C-W>j
nnoremap <C-k> <C-W>k

map <Leader>f <Action>(ReformatCode)
```

## Vscode

keybindings.json

```json
[
  {
    "key": "ctrl+cmd+f",
    "command": "editor.action.formatDocument",
    "when": "editorHasDocumentFormattingProvider && editorTextFocus && !editorReadonly"
  },
  {
    "command": "-editor.action.selectAll",
    "key": "cmd+a"
  },
  {
    "command": "editor.action.selectAll",
    "key": "cmd+a"
  },
  {
    "key": "cmd+h",
    "command": "workbench.action.splitEditorLeft"
  },
  {
    "key": "cmd+l",
    "command": "workbench.action.splitEditorRight"
  },
  {
    "key": "cmd+j",
    "command": "workbench.action.splitEditorDown"
  },
  {
    "key": "cmd+k",
    "command": "workbench.action.splitEditorUp"
  },
  {
    "key": "ctrl+shift+u",
    "command": "editor.action.transformToUppercase"
  },
  {
    "key": "ctrl+shift+i",
    "command": "editor.action.transformToLowercase"
  },
  {
    "key": "ctrl+q",
    "command": "editor.action.triggerParameterHints",
    "when": "editorHasSignatureHelpProvider && editorTextFocus"
  },
  {
    "key": "ctrl+shift+space",
    "command": "-editor.action.triggerParameterHints",
    "when": "editorHasSignatureHelpProvider && editorTextFocus"
  },
  {
    "key": "ctrl+h",
    "name": "Navigate left",
    "command": "workbench.action.navigateLeft"
  },
  {
    "key": "ctrl+j",
    "name": "Navigate down",
    "command": "workbench.action.navigateDown"
  },
  {
    "key": "ctrl+k",
    "name": "Navigate up",
    "command": "workbench.action.navigateUp"
  },
  {
    "key": "ctrl+l",
    "name": "Navigate right",
    "command": "workbench.action.navigateRight"
  },
  {
    "command": "projectManager.listGitProjects#sideBarGit",
    "key": "cmd+o"
  },
  {
    "command": "expand_region",
    "key": "ctrl+=",
    "when": "editorTextFocus"
  },
  {
    "command": "undo_expand_region",
    "key": "ctrl+-",
    "when": "editorTextFocus && editorHasSelection"
  },
  {
    "command": "workbench.action.toggleSidebarVisibility",
    "key": "ctrl+e"
  },
  {
    "command": "workbench.files.action.focusFilesExplorer",
    "key": "ctrl+e",
    "when": "editorTextFocus"
  },
  {
    "command": "explorer.newFile",
    "key": "a",
    "when": "filesExplorerFocus && !inputFocus"
  },
  {
    "command": "renameFile",
    "key": "r",
    "when": "filesExplorerFocus && !inputFocus"
  },
  {
    "command": "filesExplorer.copy",
    "key": "c",
    "when": "filesExplorerFocus && !inputFocus"
  },
  {
    "command": "filesExplorer.paste",
    "key": "p",
    "when": "filesExplorerFocus && !inputFocus"
  },
  {
    "command": "deleteFile",
    "key": "d",
    "when": "filesExplorerFocus && !inputFocus"
  },
  {
    "key": "shift+a",
    "command": "explorer.newFolder",
    "when": "explorerViewletVisible && filesExplorerFocus && !inputFocus"
  },
  {
    "key": "ctrl+j",
    "command": "workbench.action.quickOpenSelectNext",
    "when": "inQuickOpen"
  },
  {
    "key": "ctrl+k",
    "command": "workbench.action.quickOpenSelectPrevious",
    "when": "inQuickOpen"
  },
  {
    "key": "ctrl+k ctrl+o",
    "command": "workbench.action.navigateToLastEditLocation"
  },
  {
    "key": "ctrl+k ctrl+q",
    "command": "-workbench.action.navigateToLastEditLocation"
  },
  {
    "key": "cmd+r",
    "command": "editor.action.rename",
    "when": "editorHasRenameProvider && editorTextFocus && !editorReadonly"
  },
  {
    "key": "f2",
    "command": "-editor.action.rename",
    "when": "editorHasRenameProvider && editorTextFocus && !editorReadonly"
  },
  {
    "key": "ctrl+.",
    "command": "problems.action.showQuickFixes",
    "when": "problemFocus"
  },
  {
    "key": "cmd+.",
    "command": "-problems.action.showQuickFixes",
    "when": "problemFocus"
  },
  {
    "key": "ctrl+.",
    "command": "workbench.action.terminal.showQuickFixes",
    "when": "terminalFocus"
  },
  {
    "key": "cmd+.",
    "command": "-workbench.action.terminal.showQuickFixes",
    "when": "terminalFocus"
  },
  {
    "key": "ctrl+.",
    "command": "editor.action.quickFix",
    "when": "editorHasCodeActionsProvider && textInputFocus && !editorReadonly"
  },
  {
    "key": "cmd+.",
    "command": "-editor.action.quickFix",
    "when": "editorHasCodeActionsProvider && textInputFocus && !editorReadonly"
  },
  {
    "key": "escape",
    "command": "leaveEditorMessage",
    "when": "messageVisible"
  }
]
```

setting.json

```json
{
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[markdown]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[prisma]": {
    "editor.defaultFormatter": "Prisma.prisma"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.codeActionsOnSave": {
    "source.addMissingImports": true,
    "source.organizeImports": true
  },
  "editor.cursorSurroundingLines": 5,
  "editor.fontWeight": "300",
  "editor.formatOnSave": true,
  "editor.lineNumbers": "relative",
  "editor.linkedEditing": true,
  "editor.stickyScroll.enabled": true,
  "editor.suggest.insertMode": "replace",
  "editor.suggestFontSize": 14,
  "editor.wordWrap": "on",
  "errorLens.fontStyleItalic": true,
  "everforest.italicKeywords": true,
  "explorer.confirmDelete": false,
  "explorer.confirmDragAndDrop": false,
  "extensions.autoUpdate": "onlyEnabledExtensions",
  "extensions.ignoreRecommendations": false,
  "prettier.semi": true,
  "prettier.singleAttributePerLine": true,
  "prettier.singleQuote": true,
  "prettier.trailingComma": "all",
  "projectManager.git.baseFolders": ["$home/workspace"],
  "projectManager.sortList": "Recent",
  "sortJSON.orderOverride": [
    "name",
    "version",
    "main",
    "module",
    "types",
    "typings",
    "files",
    "publishConfig",
    "repository",
    "scripts",
    "prefix",
    "description",
    "body"
  ],
  "sortJSON.orderUnderride": [
    "resolutions",
    "dependencies",
    "devDependencies",
    "peerDependencies",
    "cSpell.userWords"
  ],
  "typescript.preferences.importModuleSpecifier": "relative",
  "update.showReleaseNotes": false,
  "zenMode.hideLineNumbers": false,
  "editor.guides.bracketPairs": true,
  "extensions.autoCheckUpdates": false,
  "editor.suggestSelection": "first",
  "javascript.updateImportsOnFileMove.enabled": "always",
  "files.associations": {
    "*.js": "javascript",
    "*.jsx": "javascriptreact",
    "*.wxss": "css",
    "*.wxml": "html"
  },
  "[css]": {
    "editor.tabSize": 2,
    "editor.defaultFormatter": "vscode.css-language-features"
  },
  "files.exclude": {
    "**/__pycache__": true,
    "**/.idea": true,
    "**/.project": true,
    "**/.settings": true,
    "**/.git": true,
    "**/.DS_Store": true,
    "**/dist/public": true,
    "**/tmp": true,
    "**/tags": true,
    "**/public/dist": true,
    "**/.vscode": true
  },
  "[json]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "search.followSymlinks": false,
  //  Go language settings
  "go.formatTool": "gofmt",
  "go.useLanguageServer": true,
  "[go]": {
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
      "source.organizeImports": true
    },
    // Optional: Disable snippets, as they conflict with completion ranking.
    "editor.snippetSuggestions": "none"
  },
  "[go.mod]": {
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
      "source.organizeImports": true
    }
  },
  "gopls": {
    // Add parameter placeholders when completing a function.
    "usePlaceholders": true,
    // If true, enable additional analyses with staticcheck.
    // Warning: This will significantly increase memory usage.
    "staticcheck": true,
    "completeUnimported": true, // autocomplete unimported packages
    "deepCompletion": true, // enable deep completion
    "codelenses": {
      "gc_details": true
    }
  },
  "go.lintFlags": ["-checks=all"],
  "go.toolsManagement.autoUpdate": true,
  "editor.mouseWheelZoom": true,
  "terminal.integrated.tabs.enabled": true,
  // python
  "[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.tabSize": 4,
    "editor.formatOnSave": true,
    "editor.formatOnType": true
  },
  "python.formatting.autopep8Args": [
    "--max-line-length",
    "120",
    "--aggressive",
    "--aggressive",
    "--in-place"
  ],
  "python.languageServer": "Pylance",
  "liveshare.presence": false,
  "workbench.editor.enablePreview": false,
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  "terminal.integrated.enableMultiLinePasteWarning": false,
  "diffEditor.ignoreTrimWhitespace": false,
  "editor.guides.indentation": false,
  "editor.minimap.enabled": false,
  "editor.renderWhitespace": "all",
  "editor.inlineSuggest.enabled": true,
  "[rust]": {
    "editor.defaultFormatter": "rust-lang.rust-analyzer"
  },
  "typescript.updateImportsOnFileMove.enabled": "always",
  "gitlens.codeLens.authors.enabled": false,
  "gitlens.codeLens.recentChange.enabled": false,
  "editor.cursorSmoothCaretAnimation": "on",
  "editor.smoothScrolling": true,
  "workbench.list.smoothScrolling": true,
  "editor.cursorBlinking": "smooth",
  "workbench.startupEditor": "none",
  "window.restoreWindows": "none",
  //关于vim的配置文件
  "vim.foldfix": true,
  "vim.commandLineModeKeyBindingsNonRecursive": [],
  "vim.insertModeKeyBindings": [
    {
      "before": ["k", "j"],
      "after": ["<Esc>"]
    }
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    {
      "before": ["<space>"],
      "commands": ["whichkey.show"]
    }
  ],
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      // which key
      "before": ["<leader>"],
      "commands": ["whichkey.show"]
    },
    {
      "before": ["<tab>"],
      "commands": ["workbench.action.nextEditor"]
    },
    {
      "before": ["<S-tab>"],
      "commands": ["workbench.action.previousEditor"]
    },
    {
      // show help doc when press K
      "before": ["K"],
      "commands": ["editor.action.showHover"]
    },
    {
      // undo
      "before": ["u"],
      "commands": ["undo"]
    },
    {
      // redo
      "before": ["U"],
      "commands": ["redo"]
    },
    {
      // use Tab show next buffer
      "before": ["<TAB>"],
      "commands": [":bn"]
    },
    {
      // vs -> vertical split
      "before": ["v", "s"],
      "commands": [":vs"]
    },
    {
      // ca -> code action
      "before": ["c", "a"],
      "commands": ["editor.action.quickFix"]
    },
    {
      // sp -> split
      "before": ["s", "p"],
      "commands": [":sp"]
    },
    {
      "before": ["g", "b"],
      "commands": ["workbench.action.navigateToLastEditLocation"]
    },
    {
      "before": ["g", "i"],
      "commands": ["editor.action.goToImplementation"]
    },
    {
      "before": ["g", "m"],
      "commands": ["workbench.action.gotoSymbol"]
    },
    {
      // back
      "before": ["g", "h"],
      "commands": ["workbench.action.navigateBack"]
    },
    {
      // forward
      "before": ["g", "l"],
      "commands": ["workbench.action.navigateForward"]
    },
    {
      // ]d -> next error/warning/...
      "before": ["]", "d"],
      "commands": ["editor.action.marker.next"]
    },
    {
      // [d -> previos error/warning/...
      "before": ["[", "d"],
      "commands": ["editor.action.marker.prev"]
    },
    {
      "before": ["X"],
      "commands": [":nohl"]
    }
  ],
  "vim.leader": "<space>",
  "vim.smartRelativeLine": true,
  "vim.surround": true,
  "vim.sneak": true,
  "vim.useSystemClipboard": true,
  "vim.hlsearch": true,
  "vim.ignorecase": true,
  "vim.useCtrlKeys": true,
  "vim.highlightedyank.color": "rgba(230, 97, 89, 0.7)",
  "vim.highlightedyank.enable": true,
  "vim.highlightedyank.textColor": "white",
  "vim.handleKeys": {
    "<C-a>": false
  },
  "vim.easymotion": true,
  "security.workspace.trust.untrustedFiles": "open",
  "remote.SSH.remotePlatform": {
    "rlogin.cs.vt.edu": "linux"
  },
  "editor.bracketPairColorization.enabled": true,
  "editor.fontFamily": "'Fira Code', '宋体'",
  "editor.fontSize": 16,
  "debug.console.fontFamily": "'Fira Code', '宋体'",
  "terminal.integrated.fontFamily": "'3270Medium Nerd Font Mono', '宋体'",
  "terminal.integrated.fontSize": 16,
  "editor.fontLigatures": true, // === !==
  "editor.lineHeight": 1.6,
  "editor.quickSuggestions": {
    "other": "on",
    "comments": "off",
    "strings": "on"
  },
  // "files.autoSave": "afterDelay",
  // "files.autoSaveDelay": 1000, !=
  "C_Cpp.clang_format_fallbackStyle": "Google",
  "editor.tabSize": 2,
  "window.menuBarVisibility": "toggle",
  "window.titleBarStyle": "custom",
  "[jsonc]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "better-comments.tags": [
    {
      // 未完成的代码
      "tag": "TODO",
      "color": "#fa973a",
      "strikethrough": false,
      "underline": false,
      "backgroundColor": "transparent",
      "bold": false,
      "italic": false
    },
    {
      // 表示代码需要修正
      "tag": "FIXME",
      "color": "#ff0000",
      "strikethrough": false,
      "underline": false,
      "backgroundColor": "transparent",
      "bold": false,
      "italic": false
    },
    {
      // 提示
      "tag": "HINT",
      "color": "#2faf64",
      "strikethrough": true,
      "underline": false,
      "backgroundColor": "transparent",
      "bold": false,
      "italic": false
    },
    {
      // 描述代码作用
      "tag": "NOTE",
      "color": "#00b7e4",
      "strikethrough": false,
      "underline": false,
      "backgroundColor": "transparent",
      "bold": false,
      "italic": false
    },
    {
      // 表示之后可能会出现问题
      "tag": "HACK",
      "color": "#fa973a",
      "strikethrough": false,
      "underline": false,
      "backgroundColor": "transparent",
      "bold": false,
      "italic": false
    },
    {
      // 表示这里有问题
      "tag": "BUG",
      "color": "#ff0000",
      "strikethrough": false,
      "underline": false,
      "backgroundColor": "transparent",
      "bold": false,
      "italic": false
    }
  ],
  // code runner
  "code-runner.saveAllFilesBeforeRun": true,
  "code-runner.runInTerminal": true,
  "code-runner.executorMap": {
    "javascript": "node",
    "java": "cd $dir && javac $fileName && java $fileNameWithoutExt",
    "c": "cd $dir && gcc $fileName -o bin\\$fileNameWithoutExt && cd bin && .\\$fileNameWithoutExt",
    "cpp": "cd $dir && g++ $fileName -o bin\\$fileNameWithoutExt && cd bin && .\\$fileNameWithoutExt",
    "python": "python -u",
    "ruby": "ruby",
    "go": "go run",
    "shellscript": "bash",
    "ocaml": "ocaml",
    "applescript": "osascript",
    "rust": "cd $dir && rustc $fileName && $dir$fileNameWithoutExt",
    "scheme": "csi -script",
    "haskell": "runhaskell",
    "lisp": "sbcl --script",
    "sml": "cd $dir && sml $fileName"
  },
  // gitlens
  "gitlens.defaultDateFormat": "YYYY-MM-DD hh:mm:ss",
  "gitlens.defaultDateShortFormat": "YYYY-MM-DD",
  // cpp reference
  "cppref.lang": "en",
  "cppref.searchEngine": "Google",
  // doxygen documenation generator
  // C/C++
  "C_Cpp.default.cppStandard": "c++23",
  "C_Cpp.default.cStandard": "c17",
  "C_Cpp.inlayHints.autoDeclarationTypes.enabled": true,
  "C_Cpp.inlayHints.parameterNames.enabled": true,
  "C_Cpp.inlayHints.parameterNames.suppressWhenArgumentContainsName": false,
  "C_Cpp.inlayHints.parameterNames.hideLeadingUnderscores": false,
  "C_Cpp.inlayHints.referenceOperator.enabled": true,
  "C_Cpp.inlayHints.referenceOperator.showSpace": true,
  "C_Cpp.clang_format_path": "/usr/bin/clang-format",
  "C_Cpp.clang_format_style": "Google",
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.gpuAcceleration": "off",
  "[cpp]": {
    "editor.defaultFormatter": "xaver.clang-format"
  },
  "cmake.configureOnOpen": true,
  "window.commandCenter": false,
  "redhat.telemetry.enabled": true,
  "haskell.manageHLS": "GHCup",
  "haskell.serverExecutablePath": "~/.ghcup/bin/haskell-language-server-wrapper",
  "git.autofetch": true,
  "terminal.integrated.inheritEnv": false,
  "workbench.iconTheme": "vs-nomo-dark",
  "workbench.productIconTheme": "icons-carbon",
  "workbench.colorTheme": "Dracula Soft",
  "workbench.layoutControl.enabled": false,
  "window.zoomLevel": -1,
  "files.trimTrailingWhitespace": false
}
```
