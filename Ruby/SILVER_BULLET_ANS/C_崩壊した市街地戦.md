# 崩壊した市街地戦

## 解答コード
```
N = gets.to_i
abN = []
N.times do
  ab = gets.split(' ').map(&:to_s)
  abN.push(ab)
end

N.times do |i|
  ab = abN[i][0].chars.map(&:to_i)
  if ab[0]+ab[1]+ab[2] == abN[i][1].to_i
    puts "Yes"
  elsif ab[0]*10+ab[1]+ab[2] == abN[i][1].to_i
    puts "Yes"
  elsif ab[0]+ab[1]*10+ab[2] == abN[i][1].to_i
    puts "Yes"
  else
    puts "No"
  end
end
```

## 解説
Nにgets.to_iで整数値を取得し、timesとsplit,mapを用いて複数行複数列の整数値を二次元配列で取得する<br>
timesを用いて1つずつ1桁に分解された整数値の配列を呼び出し、配列abに格納し、indexを指定して値を呼び出しながら、1桁ずつの和、1桁目✕10+2桁目+3桁目、1桁目+2桁目✕10+3桁目のいずれかがabN[i][1]に格納されている整数になる場合は"Yes",そうでない場合は"No"を出力している。