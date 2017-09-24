---
title: awk
date: 2017-09-24 17:38:47
tags:
---

### awk-test内容

Beth 4.00 0
Dan 3.75 0
Kathy 4.00 10
Mark 5.00 20
Mary 5.50 22
Susie 4.25 18



### 1.打印字段数多于 4 个的输入行

``` 
NF > 4
```

### 2.打印最后一个字段值大于 4 的输入行

```
$NF > 4 
```

### 3.打印所有输入行的字段数的总和

```awk
{ nf = nf + NF } END { print nf } 
```


### 4.打印包含 Beth 的行的数量

```awk
/Beth/ { nlines = nlines + 1 } END { print nlines }
```
### 5.打印具有最大值的第一个字段, 以及包含它的行 (假设 $1 总是 正的) 18

```awk
$1 > max { max = $1; maxline = $0 } END { print max, maxline }
```
### 6.打印至少包含一个字段的行

```awk
NF > 0
```
### 7.打印长度超过 80 个字符的行

```awk
length($0) > 80
```
### 8.在每一行的前面加上它的字段数

```awk
{ print NF, $0 }
```
### 9.打印每一行的第 1 与第 2 个字段, 但顺序相反

```awk
{ print $2, $1 }
```
### 10.交换每一行的第 1 与第 2 个字段, 并打印该行

```awk
{ temp = $1; $1 = $2; $2 = temp; print }
```
### 11.将每一行的第一个字段用行号代替

```awk
{ $1 = NR; print }
```
### 12.打印删除了第 2 个字段后的行

```awk
{ $2 = ""; print }
```
### 13.将每一行的字段按逆序打印

```awk
{ for (i = NF; i > 0; i = i - 1) printf("%s ", $i) printf("\n")}
```
### 14.打印每一行的所有字段值之和

```awk
{ sum = 0
  for (i = 1; i <= NF; i = i + 1) 
      sum = sum + $i
      print sum 
}
```
### 15.将所有行的所有字段值累加起来

```awk
{ for (i = 1; i <= NF; i = i + 1) 
    sum = sum + $i } 
  END { print sum }
```
### 16.将每一行的每一个字段用它的绝对值替换

```awk
{ for (i = 1; i <= NF; i = i + 1) 
      if ($i < 0) $i = -$i 
      print 
}
```
### 17.判断是否有重复

```awk
awk '++a[$1]>1{print "duplicate";exit}'
```
### 18.拿出相同的字段

```awk
awk '{a[$1]++}END{for(i in a)if(a[i]>1)print i}'
```
### 19.搜索每小时工资最高的雇员

```awk
$2 > maxrate { maxrate = $2; maxemp = $1 } 
END { 
	print "highest hourly rate:", maxrate, "for", maxemp 
}
```


### 20.利用 NR 来计算平均报酬

```awk
{ pay = pay + $2 * $3 } 
END { 
	print NR, "employees" print "total pay is", pay print "average pay is", pay / NR
}
```


### 21.字符串拼接，输出所有人名

```awk
{ names = names $1 " " } END { print names }
```


### 22.虽然在 END 动作里, NR 的值被保留了下来, 但是 $0 却不会,打印最后一行

```awk
awk '{ last = $0 } END { print last }'
```
### 23.使用 length, NF 与 NR 计算行, 单词与字符的数量, 为方便起见, 我们将每个字段都当成一个单词

```awk
awk '{ nc = nc + length($0) + 1; nw = nw + NF } END { print NR, "lines,", nw, "words,", nc, "characters" }'
```


### 24.计算每小时工资多于 $6.00 的雇员的总报酬与平均报酬. 在计算平均数时, 它用到了if 语句, 避免用 0 作除数

```awk
awk '$2 > 6 { n = n + 1; pay = pay + $2 * $3 } 
END { 
        if (n > 0) print n, "employees, total pay is", pay,"average pay is", pay/n
	else print "no employees are paid more than $6/hour"
     }'
```
### 25.输入行的总行数

```awk
END { print NR }
```
###26.打印第 10 行

```awk
NR == 10
```
### 27.打印每一个输入行的最后一个字段

```awk
{ print $NF }
```
### 28.打印最后一行的最后一个字段

```awk
{ field = $NF }
END { print field }
```


