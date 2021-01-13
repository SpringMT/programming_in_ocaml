## 章


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

```
