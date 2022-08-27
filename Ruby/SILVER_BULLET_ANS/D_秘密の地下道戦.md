# 秘密の地下道戦

## 解答コード
```
a = gets.to_i
b = gets.to_i

for i in a+1..b-1
  puts i
end
```

## 解説
aとbにそれぞれgets.to_iで整数値を取得し、aより大きくb未満の数をfor文の a+1 ~ b-1 の範囲を用いて出力する。