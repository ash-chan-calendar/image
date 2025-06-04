
## 機能2. **リポジトリへの画像をwebpへ変換 (GitHub Actions)**
### 要件

#### 1. 対象ファイル

**対象リポジトリ:** このリポジトリ
actionsを動かすブランチ: add-image

**ファイル構成例:**
```
image/
├── 20240101.png    ← 変換対象
├── 20240102.png    ← 変換対象  
├── 20240301.png    ← 変換対象
├── ...
├── 20250101.png    ← 変換対象
├── file_blacklist.txt  ← 除外
└── README.md       ← 除外
```

#### 2.  pngフォルダへ移動(手動)
image/に画像があったら、image/png/に画像を移動させる

**変換対象:**
- image/png/ に配置されている画像ファイル（jpg, jpeg, png, gif）
- 拡張子と実際のファイル形式が異なる場合も対応（例: .png拡張子のjpgファイル）
- 新規追加された画像ファイルを自動検知
- webp形式以外の画像ファイルが対象
- `file_blacklist.txt`, `README.md` などのテキストファイルは除外
- webp→webpフォルダへ
- png→pngフォルダへ

#### 2. 変換機能
- 元画像をwebp形式に変換
- imagemagickを使用して実装
- 画質設定:　70%
- 1ファイル2MB以下にして
- 元ファイルは保持
- 変換後のファイル名: `元ファイル名.webp`

#### 3
- bashで実装してみて
- シンプルに見やすく処理を書いて
<!-- - bash と pythonで書くのどっちがいい？ -->

#### 3. 実行タイミング
- 手動トリガー

#### 4. 出力
- 変換結果をコミット・プッシュ
  - ghでシンプルに実装

#### 5. Actions作成
- .github\workflows
- [WebP変換Actions](/.github/workflows/convert-to-webp.yml)
- ImageMagickを使用（cwebpより高機能な変換オプション）
- file_blacklist.txt対応（除外ファイル指定可能）
  - 1行1ファイル名
- .github/workflows/pr-check-rename.ymlを参考にしてみて
  - ファイルは存在する

### 実装
- できるだけシンプルに実装
- 日本語のコメントを分節ぐらいに書いてわかりやすく