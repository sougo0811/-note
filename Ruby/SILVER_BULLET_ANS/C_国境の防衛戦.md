# 国境の防衛戦

## 解答コード
```
N = gets.to_i
SN = []
N.times do |i|
  SN[i] = gets.split("//")
end

N.times do |j|
  if SN[j][0] != ""
    puts(SN[j][0])
  else
    puts("\n")
  end
end
```
## 解説
gets.to_iでNを取得し、繰り返し処理のtimesを使って配列SNに入力された文字列を追加していく。このとき、splitを用いて"//"があるところで文字列を区切って追加することによって、問題文の条件を満たす文字列を取得する。<br>
出力するときは、同じくtimesを用いて、条件を満たす文字列を保存したS[j][0]の値を出力する。このとき、S[j][0]の値がない場合を除外する。