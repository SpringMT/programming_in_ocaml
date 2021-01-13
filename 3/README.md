## 章

```
let fib n =
 let rec fib_pair n =
  if n = 1 then (1,0)
  else
   let (i, j) = fib_pair(n - 1) in
     (i + j, i)
 in
   let (i, _) = fib_pair n in
     i
     ;;
#trace fib;;
fib 8;;
#untrace fib;;
```


## 練習問題
* 参照
  * https://ymotongpoo.hatenablog.com/entry/20100320/1269103997
  * https://github.com/kaznum/programming_in_ocaml_exercise

### 3-1-1

```
let yen_of_dollar d = 
  let rate = 114.32 in
  int_of_float (d *. rate +. 0.5);;

114 = yen_of_dollar 1.;;
```

### 3-1-2
```
let dollar_of_yen yen = 
  let rate = 114.32 in
  floor(float_of_int (yen) /. rate *. 100. +. 0.5) /. 100. ;;

0.09 = dollar_of_yen 10;;
```

### 3-1-3

```
let yen_doller_string dollar =
  let yen_of_dollar d = 
    let rate = 114.32 in
      int_of_float (d *. rate +. 0.5) in
  string_of_float (dollar) ^ " dollars are " ^ string_of_int (yen_of_dollar dollar) ^ " yen.";;

"2. dollars are 229 yen." = yen_doller_string 2.0 ;;
```

### 3-1-4

```
let capitalize c =
  let char_int = int_of_char c in
    (*
      # int_of_char 'a';;
        - : int = 97
      # int_of_char 'z';;
        - : int = 122
    *)
    (* 'a' <= ch && ch <= 'z' *)
    if char_int >= 97 && char_int <= 122 then
      char_of_int (char_int - 32)
    else
      c
      ;;
'A' = capitalize 'a';;
'O' = capitalize 'o';;
'B' = capitalize 'B';;
'1' = capitalize '1';;
```
### 3-2

```
(* if b1 then *)
if b1 = true then
  b2
else
  false;;
```

```
if b1 = true then
  true
else
  b2;;
```

### 3-3
```
let answer_and b1 b2 =
  if not (not b1 || not b2) then true else false;;
true = answer_and true true;;
false = answer_and false false;;
false = answer_and true false;;
false = answer_and false true;;

let answer_or b1 b2 =
  if not (not b1 && not b2) then true else false;;
true = answer_or true true;;
false = answer_or false false;;
true = answer_or true false;;
true = answer_or false true;;
```

### 3-4
```
let x = 1 in let x = 3 in let x = x + 2 in x * x;;
                                  x = 3    x = 5
25
let x = 2 and y = 3 in (let y = x and x = y + 2 in x * y) + y;;
                                                  y = 2  x = 5
13
let x = 2 in let y = 3 in let y = x in let z = y + 2 in x * y * z;;
                              y =2         z = 4        2 * 2 * 4
16

# let x = 1 in let x = 3 in let x = x + 2 in x * x;;
Warning 26: unused variable x.
- : int = 25
# let x = 2 and y = 3 in (let y = x and x = y + 2 in x * y) + y;;
- : int = 13
# let x = 2 in let y = 3 in let y = x in let z = y + 2 in x * y * z;;
Warning 26: unused variable y.
- : int = 16
```
### 3-5

```
let x = e1 and y = e2;;
xがe1 yがe2としてトップレベルに束縛される
しかし、xの参照ができない
# let x = 1 and y = x+3;;
Error: Unbound value x

let x = e1 let y = e2;;
xはe1としてトップレベルに束縛される
yはトップレベルとして参照できる、xが束縛された後に実行されるためxも参照可能
# let x = 1 let y = x+3;;
val x : int = 1
val y : int = 4
# y
  ;;
- : int = 4

```

### 3-6
```
let geo_mean (x, y) =
  sqrt(x *. y);;
4.0 = geo_mean (1., 16.);;
```
```
let bmi (name, sintyo, taiju) =
  let bmi_score = taiju /. (sintyo ** 2.) in
    if bmi_score < 18.5 then
      name ^ "さんはやせています"
    else if bmi_score >= 18.5 && bmi_score < 25.0 then
      name ^ "さんは標準です"
    else if bmi_score >= 25.0 && bmi_score < 30.0 then
      name ^ "さんは肥満です"
    else
      name ^ "さんは高度肥満です"
      ;;

"hogeさんはやせています" = bmi ("hoge", 170.0, 50.0);;
```

```
let sum_and_diff (x, y) = 
  (x + y, x - y);;
let f (a, b) =
  ((a + b) / 2, (a - b) / 2);;
(2,4) = f(sum_and_diff(2,4));;
```

### 3-7
```
let rec pow (x, n) =
  if n = 0 then
    1
  else
    x * pow(x, n-1)
    ;;
16 = pow (2, 4);;

let rec pow2 (x, n) = match n with
  0 -> 1
  | 1 -> x
  | n when n mod 2 = 0 -> 
    let res = pow2(x, n /2) in 
      res * res
  | _ -> let res = pow2(x, n /2) in
    res * res * x
    ;;
  16 = pow2 (2, 4);;
```

### 3-8
```
let rec interpow(x, n, res) =
 if n = 0 then
   res
 else
  interpow(x, n - 1, res * x)
  ;;
16 = interpow(2, 4, 1);;
````

### 3-11

```
(* 目的 : 2つの自然数 m と nの最大公約数を求める *)
(* gcd : int -> int -> int *)

(* 自明なケース n = 0ならばmが最大公約数 *)
(* 再帰停止性 : nと mをnで割った余り の最大公約数が答え  n の値が小さくなっているので、いずれ 0 になり停止する*)
let gcd m n =
  
```

### 3-10
