# 森林の塹壕戦

## 解答コード
```
N,T = gets.split(' ').map(&:to_i)
pxN = []
N.times.map do
  px = gets.split(' ').map(&:to_i)
  pxN.push(px)
end

exp = 0
while T != 0
  exp += pxN[T-1][1]
  T = pxN[T-1][0]
end

puts exp
```

## 解説
times文で、親スキルと必要経験値を取得し、while文でスキルツリーを子から親へと逆算しながら、必要経験値を加算していく。<br>二次元配列のTの値を用いてスキル獲得に必要な経験値を探索し、その後Tの値をその親の値へと上書きする。<br>
解答コードの場合、pxN[][1]がスキル獲得に必要な経験値でpxN[][0]が獲得したスキルの親スキルの保存場所を保管している。