# 黒煙の戦車戦

## 解答コード
```
H, W, K = gets.split(' ').map(&:to_i)
amidas = []
H.times.map do
  amida = gets.chomp.split('')
  amidas.push(amida)
end

start = amidas[0].index(K.to_s)
np = start
(H-2).times.map do |i|
  while 0 < np && amidas[i+1][np-1] == "."
    np -= 1
    amidas[i+1][np] = "#"
  end
  while np < W && amidas[i+1][np+1] == "."
    np += 1
    amidas[i+1][np] = "#"
  end
end

puts amidas[H-1][np]
```

## 解説
timesとmap,splitを用いて二次元配列であみだくじの情報を取得する。<br>
スタート地点のインデックスを取得し、times文で行を加算しながらwhile文で行内の通れる道である"."があるとき、現在地を保存する変数を更新していく。while文は左に移動と右に移動の２パターン作る。また一度通った道を通らないようにするために、道を通った後に壁である"#"に変更していく。<br>
最後に現在地の変数をインデックスとした配列の最後尾の数を出力する。<br>