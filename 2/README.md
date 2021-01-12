## 2-1
```
        OCaml version 4.11.1

# - - 1;;
- : int = 1
# - 2+3;;
- : int = 1
# 9 / -4
  ;;
- : int = -2
# +3 + 5;;
- : int = 8
```

## 2-2
```
# float_of_int 3 +. 2.5 ;;
- : float = 5.5
# int_of_float 0.7;;
- : int = 0
# char_of_int((int_of_char 'A') + 20);;
- : char = 'U'
# int_of_string "0xff";;
- : int = 255
# 5.0 ** 2.0;;
- : float = 25.
```

## 2-3
```
8*-2
*- が 中置演算子とみなされ構文エラー
# 8*-2;;
Error: Unbound value *-

int_of_string "0xfg"
例外エラー
16進数でgがでてこない

# int_of_string "0xfg";;
Exception: Failure "int_of_string".

int_of_float -0.7
構文エラー
-だとfloatに対してのintの四則演算とみなされる

# int_of_float (-.0.7);;
- : int = 0
```

## 2-4

```
"float_of_int int_of_float 5.0 ⇒ 5.0"

# float_of_int (int_of_float 5.0);;
- : float = 5.

sin 3.14 /. 2.0 ** 2.0 +. cos 3.14 /. 2.0 ** 2.0;;

# sin (3.14 /. 2.0) ** 2.0 +. cos (3.14 /. 2.0) ** 2.0;;
- : float = 1.

sqrt 3 * 3 + 4 * 4;;
# sqrt (float_of_int (3 * 3 + 4 * 4));;
- : float = 5.
```
