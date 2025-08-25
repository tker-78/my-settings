# 🎮 Steam ゲーム起動エラー対応 (Ubuntu + NVIDIA)
*作成日: 2025-08-24*

## 1. 課題
- Steamでゲームを起動すると **「DX12 is not supported」** エラーが出る  
- `vulkaninfo` の出力が **llvmpipe (ソフトウェアVulkan)** になっていて GPU が使われていない  
- Steam が **「Downloading Content (0%)」** のまま止まる  

---

## 2. 対策
### 2.1 NVIDIAドライバ導入
```bash
ubuntu-drivers devices
sudo apt install nvidia-driver-575-open
sudo reboot
```

### 2.2 Vulkan関連ライブラリの導入
```bash
sudo apt install vulkan-tools libvulkan1 libvulkan1:i386 \
mesa-vulkan-drivers mesa-vulkan-drivers:i386
```

### 2.3 動作確認
```bash
vulkaninfo | grep "driver"
# driverName = NVIDIA が出ればOK
```

### 2.4 Steam / Proton設定
- Steam → ライブラリ → ゲーム → プロパティ → **互換性**
  - Proton Experimental または Proton GE を選択
- 起動オプション例
  ```
  -dx11
  -force-vulkan
  ```

### 2.5 GPU使用確認
```bash
watch -n1 nvidia-smi
# ゲーム実行中にプロセスが表示されればGPU利用中
```

---

## 3. 抽象化（一般化した手順）
LinuxでSteamゲームが動かない場合は次を確認：

1. **GPUドライバ**  
   - `ubuntu-drivers devices` → 推奨ドライバをインストール
2. **Vulkan環境**  
   - `vulkaninfo` → `driverName = NVIDIA/AMD/Intel` を確認
3. **32bitライブラリ**  
   - `libvulkan1:i386` などを追加
4. **Steam設定**  
   - Protonバージョン切り替え / 起動オプション変更
5. **GPU使用確認**  
   - `nvidia-smi` でプロセスが動いているか確認

---

✅ まとめ:  
LinuxでSteamゲームが起動しないときは  
**「GPUドライバ → Vulkan → ライブラリ → Proton設定」** の順でチェックする。
