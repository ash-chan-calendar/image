## 機能2. **リポジトリへの画像をwebpへ変換 (GitHub Actions)**
### actions url
- [https://github.com/ash-chan-calendar/image/actions](https://github.com/ash-chan-calendar/image/actions)
### 要件


#### 1. 対象ファイル

**対象リポジトリ:** このリポジトリ
**actionsを動かすブランチ:** dev-webp（実装済みはadd-imageブランチ）

**ファイル構成例:**
```
image/
├── png/                     ← 変換元フォルダ
│   ├── 20240101.png        ← 変換対象
│   ├── 20240102.jpg        ← 変換対象  
│   └── 20240301.gif        ← 変換対象
├── webp/                   ← 変換先フォルダ（自動作成）
│   ├── 20240101.webp       ← 変換後
│   ├── 20240102.webp       ← 変換後
│   └── 20240301.webp       ← 変換後
├── file_blacklist.txt      ← 除外ファイルリスト
└── README.md               ← 除外
```

#### 2. フォルダ構成と処理フロー
**事前準備:**
- `image/` 直下に画像があった場合、`image/png/` に移動

**変換対象:**
- `image/png/` に配置されている画像ファイル（jpg, jpeg, png, gif）
- 拡張子と実際のファイル形式が異なる場合も ImageMagick で自動判定
- webp形式以外の画像ファイルが対象
- 既に `image/webp/` に同名のwebpファイルが存在する場合はスキップ

**除外対象:**
- `image/file_blacklist.txt` に記載されたファイル（1行1ファイル名）
- 既存のwebpファイル

**フォルダ作成:**
- `image/png/`, `image/webp/` フォルダが存在しない場合は自動作成

#### 3. 変換機能
- **変換ツール:** ImageMagick (`magick` コマンド)
- **画質設定:** 70%（初期値）
- **ファイルサイズ制限:** 2MB以下
- **サイズ調整:** 2MBを超える場合は画質を10%ずつ下げて再変換（最低30%まで）
- **元ファイル:** `image/png/` に保持
- **変換後ファイル名:** `元ファイル名.webp`（拡張子のみ変更）

##### 技術仕様
- **変換コマンド:** `magick input -quality 70 output.webp`
- **サイズ制限処理:** 2MB超過時は画質を段階的に30%まで下げて再変換
- **ブラックリスト形式:** `image/file_blacklist.txt` に1行1ファイル名で記載
- **対応形式:** JPG, JPEG, PNG, GIF → WebP
- **スキップ条件:** 既存WebPファイル、ブラックリスト記載ファイル、出力ファイル既存

#### 4. 実行タイミング
- **手動トリガー:** `workflow_dispatch`
- **ドライラン機能:** プレビューモード付き

#### 5. 出力・コミット
- **変換結果:** `image/webp/` フォルダに保存
- **自動コミット:** 変更があった場合のみ実行
- **コミットメッセージ:** 変換件数を含む詳細メッセージ
- **プッシュ:** 同じブランチに自動プッシュ

#### 6. GitHub Actions設定
- **ファイル場所:** `.github/workflows/Convert-Images-to-WebP.yml`
- **実行環境:** ubuntu-latest
- **権限:** contents: write, pull-requests: write
- **参考実装:** `.github/workflows/pr-check-rename.yml` の構造を参考

### 実装状況
- ✅ GitHub Actions ワークフローファイル作成済み (`.github/workflows/Convert-Images-to-WebP.yml`)
- ✅ ImageMagick を使用したBash実装
- ✅ ブラックリスト機能対応 (`image/file_blacklist.txt`)
- ✅ ドライラン機能実装
- ✅ 自動コミット・プッシュ機能
- ✅ ファイルサイズ制限と画質調整機能
- ✅ 日本語コメント付きで見やすい実装
- ✅ 実行結果サマリー機能

### 使用方法
1. `image/png/` に変換したい画像を配置
2. GitHub の Actions タブから「Convert Images to WebP」を手動トリガー
3. 必要に応じて「Dry run」オプションを有効にしてプレビュー確認
4. 変換完了後、`image/webp/` フォルダに結果が保存され、自動でコミット・プッシュされる