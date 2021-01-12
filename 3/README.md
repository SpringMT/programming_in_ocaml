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

