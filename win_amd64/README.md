# Windows AMD_64

## インストールするソフトウェア
- Docker Desktop
- Google Chrome
- Microsoft Office
- VS Code
- SinatraPDF
- WSL
- scoop
- oh-my-posh
- PostgreSQL
- Vim
- Power Toys


## WSLのインストール

```ps
$ wsl --install
```

## Scoopのインストール
Scoopのページを参照。

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

```ps
scoop install sudo
sudo scoop install 7zip git openssh --global
scoop install aria2 curl grep sed less touch
scoop install python ruby go perl
scoop install vim
```

## oh-my-poshのインストール
```ps
$ winget install JanDeDobbeleer.OhMyPosh -s winget
$ scoop install https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/oh-my-posh.json
```
一度再起動する。

fontのインストール
```ps
$ oh-my-posh font install # mesloを選択する
```

vscodeの統合ターミナルで文字化けするので設定する。
vscodeの設定`Ctl+,`で`Integrated:font`で検索し、
`font family`に`インストールしたフォントを指定する。

## oh-my-poshのテーマの変更

```bash
$ Get-PoshThemes
```


```bash
$ vim $PROFILE
```

```vim
oh-my-posh init pwsh --config "C:\Users\kktak\AppData\Local\Programs\oh-my-posh\themes\1_shell.omp.json" | Invoke-Expression
```

```ps
$ . $PROFILE
```



## VS Codeプラグイン
- vim
- Markdown All in One
- Docker
- PostgreSQL(Chris Kollman)
- Tabnine



## PowerToysの設定

- キーマッピングの設定
