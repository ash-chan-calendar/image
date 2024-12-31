# README

## アップロードしやすい方法を考えよう
Githubに入れる前に画像のサイズを10MB以下にしないとファイルのアップロードができずにコケる
LFSでは1リポジトリあたり、合計1GB以下に抑える必要があるため、運営を続けるに当たり微妙

- Google Drive → Github



## ffmpeg
./* に入力パス
以下 変換したい画像群のエクスプローラー画面でopen git bash here をクリックし、実行

for img in [入力path]/*; do ffmpeg -i "$img" -qscale:v 2 -update 1 [出力path]/"$(basename "${img%.*}").jpg"; done

aというディレクトリを作成後
for img in ./*; do ffmpeg -i "$img" -qscale:v 2 -update 1 ./a/"$(basename "${img%.*}").jpg"; done
