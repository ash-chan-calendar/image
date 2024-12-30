# README

## ffmpeg
./* に入力パス
以下 変換したい画像群のエクスプローラー画面でopen git bash here をクリックし、実行

for img in [入力path]/*; do ffmpeg -i "$img" -qscale:v 2 -update 1 [出力path]/"$(basename "${img%.*}").jpg"; done

aというディレクトリを作成後
for img in ./*; do ffmpeg -i "$img" -qscale:v 2 -update 1 ./a/"$(basename "${img%.*}").jpg"; done
