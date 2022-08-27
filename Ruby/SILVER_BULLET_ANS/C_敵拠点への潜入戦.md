## 敵拠点への潜入戦

## 解答コード
```
S = gets.chomp.split('').map(&:to_i)
N = gets.to_i
xyN = []
N.times do
  xy = gets.split(' ').map(&:to_i)
  xyN.push(xy)
end

for i in 0..N-1 do
  for j in (xyN[i][0]-1)...xyN[i][1] do
    if S[j] == 0
      S[j] = 1
    else
      S[j] = 0
    end
  end
end

print(S.join)
```

## 解説
Sにgets.chomp.split('').map(&:to_i)を用いて受信した記号を1桁ごとの整数値の配列として取得する。(chompをつけないと一桁増えてしまうので注意)<br>
Nにgets.to_iで整数値を取得する。<br>
timesとsplit,mapを用いて複数行複数列の値を二次元配列で取得する。<br>
外側のfor文で中継所を1つずつ呼び出し、内側のfor文で中継所で0と1をひっくり返す範囲を一つずつ呼び出している。またif文により0→1,1→0にしている。<br>
最後に解読された数値の配列をjoinを用いて文字列に変換して出力している。<br>
