# ひび割れた大地戦

## 解答コード
```
H,W,X = gets.split(' ').map(&:to_i)
s_HW = [[]*W]
H.times do |i|
  s_HW[i] = gets.split(' ').map(&:to_i)
end

if 0 < X-1
  pin_min = X-2
elsif
  pin_min = X-1
end
if X-1 < W
  pin_max = X
elsif
  pin_max = X-1
end


pin_cnt = s_HW[0][X-1]
(H-1).times do |i|
  for j in pin_min..pin_max do
    pin_cnt += s_HW[i+1][j]
  end
  if 0 < pin_min
    pin_min -= 1
  end
  if pin_max < W-1
    pin_max += 1 
  end
end

puts pin_cnt
```


## 解説
timesとmap,splitを用いて二次元配列でピンの情報を取得する。<br>
得点と倒れるピンの領域を変数を使って管理し、times文で１行ごと取り出し、その行の倒れるピンの領域内にあるピンの得点をfor文で得点の変数に加算していく。<br>
その後、倒れるピンの領域が配列の範囲内であれば、外側に拡大していく。<br>