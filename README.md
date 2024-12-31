# README

## アップロードしやすい方法を考えよう
### Githubのアップロード仕様
公式ドキュメントには書いてないもので、アップロード不可になっている可能性があるので検証が必要
検証①　51MBのファイルをプッシュできるか?
検証②　1ファイル10MBより小さい複数ファイルで101MBをプッシュできるか?

- ❓Githubに入れる前に画像のサイズを10MB以下にしないとファイルのアップロードができずにコケる(ココらへんの条件が不明確)
- 1ファイル100MB超えるとプッシュできない(https://docs.github.com/ja/repositories/working-with-files/managing-large-files/about-large-files-on-github)
- ❓一度にコミットするファイルの合計サイズは 50 MB に制限されます。
- 1リポジトリの容量制限はない
LFSでは1リポジトリあたり、合計1GB以下に抑える必要があるため、運営を続けるに当たり微妙

### 画像圧縮検討
検証① Actionsの一時ストレージで画像を変換できるのか?
調査① GASで画像圧縮できるのか?

GASを書く気がしない
ActionsでPython動かせばいいか

- Google Drive → Github
- ❌ Google Drive内で画像圧縮 → Github (Driveに圧縮する機能がない Photoでは圧縮できるっぽい)
- Google Drive → GASで画像圧縮 → Github
- ⭕? Google Drive → Github Actionsで画像圧縮 → Github
- Google Drive → 画像圧縮 → Github
- クライアントPCで画像圧縮 → Github



## ffmpeg
./* に入力パス
以下 変換したい画像群のエクスプローラー画面でopen git bash here をクリックし、実行

for img in [入力path]/*; do ffmpeg -i "$img" -qscale:v 2 -update 1 [出力path]/"$(basename "${img%.*}").jpg"; done

aというディレクトリを作成後
for img in ./*; do ffmpeg -i "$img" -qscale:v 2 -update 1 ./a/"$(basename "${img%.*}").jpg"; done
