# Ubuntu server24.04 LTS + i3WM

VM型の軽量GUI構成のセッティング手順を記録する。

## インストールするソフトウェア

- lightdm




## 環境構築

```
sudo apt install lightdm i3-wm i3status i3lock dmenu
sudo apt install fcitx5 fcitx5-mozc
sudo apt install xrandr arandr
```

### 設定ファイルのコピー
```bash
ls -d ~/.config/i3
mkdir -p ~./config/i3 #フォルダがなければ作る
cp /etc/i3/config ~/.config/i3/config
```

```bash
sudo systemctl restart lightdm
```


### Metaキーの割当て

- `~/.config/i3/config`を編集する。
```bash
set $mod Mod4 # デフォルトではMod1(Alt)
```
- Mod1を`$mod`に書き換える。




### 日本語入力設定

```bash
sudo apt install fcitx5 fcitx5-mozc fcitx5-config-qt dbus-x11
sudo apt install fcitx5-frontend-gtk3 fcitx5-frontend-qt5 # optional
```

.Xprofile
```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
export DefaultIMModule=fcitx
```

- .config/i3/configに追記
```bash
exec --no-startup-id fcitx5 -d
```

- 変換/無変換に日本語切り替えを割り当て
```bash
fcitx5-config-qt
```
- MOXC -> settings -> keymap customize
- Direct input: Henkan -> set input mode to Hiragana
- 他: Muhenkan -> Deactivate IME


### Locale設定

```bash
sudo apt install fonts-noto-cjk
```

```bash
sudo locale-gen en_US.UTF-8
sudo update-locale LANG=en_US.UTF-8 
```

**en_USをつかっているのは、ja_JPを使うと文字幅が全角サイズになってしまうから。**


### ターミナルの設定

デフォルトではxterm。

```bash
sudo apt install alacritty
```

.config/i3/config
```bash
bindsym $mod+Return exec alacritty
```

- 日本時間に変更
```bash
sudo timedatectl set-timezone Asia/Tokyo
```


### dmenuへのアイテム追加

.bashrc
```bash
export PATH="./.local/bin:$PATH"
```

対象の実行ファイルへのシンボリックリンクをを上記PATHに置く。

```bash
ln -s /path/to/target ~/.local/bin/
```


#### Obsidian

AppImage版を~/Applicationsにインストールする。

~/.local/bin/obsidian
```bash
#!bin/bash
exec $HOME/Applications/Obsidian.<version>.AppImage --no-sandbox "$@"
```


























