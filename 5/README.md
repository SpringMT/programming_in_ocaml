```
let rec reverse = function
  [] -> []
  | first::rest -> (reverse rest) @ [first]
  ;;
let test1 = reverse [1;2;3;4] = [4;3;2;1];;

let rec revAppend l1 l2 = 
  match l1 with
  [] -> l2
  | first::rest -> revAppend rest (first :: l2)
  ;;
let rev l = revAppend l [];;
let test1 = rev [1;2;3;4] = [4;3;2;1];;
```

挿入ソート

```
let rec insert x = function
  [] -> [x]
  | first::rest -> 
    if x < first then
      x :: (first :: rest)
    else
      first :: (insert x rest)
    ;;
let test1 = insert 3 [1;2;3;4;5] = [1; 2; 3; 3; 4; 5];;

let rec insert2 x = function
  [] -> [x]
  | first::rest when x < first -> x :: (first :: rest)
  | first::rest -> first :: (insert x rest)
    ;;
let test2 = insert2 3 [1;2;3;4;5] = [1; 2; 3; 3; 4; 5];;

let rec insertion_sort = function
  [] -> []
  | first::rest -> insert first (insertion_sort rest)
;;

let test3 = insertion_sort [1;2;5;4;3] = [1; 2; 3; 4; 5];;
```

```
let rec partition pivot = function
  [] -> ([], [])
  | first::rest ->
    let (left, right) = partition pivot rest in
      if first < pivot then
        (first::left, right)
      else
        (left, first::right)
        ;;
let test4 = partition 7 [9; 1; 5; 4; 18] = ([1;5;4],[9;18;]);;
```

## 練習問題
### 5.2
```
let rec downto1 = function
  0 -> []
  | a -> a :: downto1 (a-1)
  ;;
```

```
let rec roman_repeat roman_str = function
  0 -> ""
  | n -> roman_str ^ roman_repeat roman_str (n - 1)
  ;;

let rec roman dict num =   
  match dict with
    [] -> ""
    | (n, roman_str)::rest ->
      let count = num / n
        in
          (roman_repeat roman_str count) ^ roman rest (num mod n)
          ;;
```

```
let rec nested_length = function
  [] -> 0
  | [] :: rest -> nested_length rest
  | (_::rest1) :: rest2 -> 1 + nested_length(rest1::rest2)
  ;;
```

```
let rec concat = function
  [] -> []
  | [] :: rest -> concat rest
  | (n::rest1) :: rest2 -> n :: concat(rest1::rest2)
  ;;

こういうのもある

# let concat = List.fold_left (@) [];; 
val concat : '_weak1 list list -> '_weak1 list = <fun>
# concat [[0; 3; 4]; [2]; []; [5; 0]];;
- : int list = [0; 3; 4; 2; 5; 0]
# [0; 3; 4] @ [2];;
- : int list = [0; 3; 4; 2]
```

```
let rec zip a b =
  match (a, b) with
    (_, []) | ([], _) -> []
    | (a'::rest_a, b'::rest_b) -> (a', b') :: zip rest_a rest_b
    ;;

zip[2;3;4;5;6;7;8;9;10;11]
        [true; true; false; true; false; true; false; false; false; true];;
```

```
let rec unzip lst =
  match lst with
    [] -> ([], [])
    | (a, b) :: rest -> (a:: (fst (unzip rest)), b:: snd( (unzip rest)))
    ;;
unzip(zip[2;3;4;5;6;7;8;9;10;11]
             [true; true; false; true; false; true;
             false; false; false; true]);;
```

```
let rec filter x lst =
  match lst with
    [] -> []
    | (a :: rest) when x a -> a :: filter x rest
    | a :: rest -> filter x rest
    ;;
    
let is_positive x = (x > 0);;
filter is_positive [-9; 0; 2; 5; -3];;

filter (fun l -> length l = 3) [[1; 2; 3]; [4; 5]; [6; 7; 8]; [9]];;
```

```
let rec take n lst =
  match lst with
  [] -> []
  | (a::rest) when n > 0 -> a :: (take [@tailcall]) (n-1) rest
  | _ -> []
  ;;
#trace take;;

let rec take n lst =
  match (n, lst) with
  (0, _) | (_, []) -> []
  | (n, a::rest) -> a :: take (n-1) rest
  ;;

let rec drop n lst =
  match (n, lst) with
  (0, _) | (_, []) -> lst
  | (n, a::rest) -> drop (n-1) rest
  ;;

let ten_to_zero = [10; 9; 8; 7; 6; 5; 4; 3; 2; 1];;
take 8 ten_to_zero;;
drop 7 ten_to_zero;;
```

```
let max_list lst = 
  let rec imax_list max lst =
    match lst with
      [] -> max
      | (a :: rest) when a > max  -> imax_list a rest
      | (a :: rest) -> imax_list max rest
  in
    match lst with
    a :: rest -> (imax_list [@tailcall]) a rest
    ;;
#trace max_list;;
max_list [7; 9; 0; -5];;
```



