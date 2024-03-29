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
#trace max_list;;,
max_list [7; 9; 0; -5];;
```

### 5.3
https://www.ocaml.org/releases/4.01/htmlman/libref/Pervasives.html

```
let rec mem a s =
  match s with
  [] -> false
  | (x::rest) when x = a -> true
  | (x::rest) -> (mem[@tailcall]) a rest
  ;;

mem 3 [1;2;3;4;5];;
mem 6 [1;2;3;4;5];;

let rec intersect s1 s2 =
  match s1 with
  [] -> []
  | (a::rest) when mem a s2 -> a:: ((intersect[@tailcall]) rest s2)
  | (a::rest) -> (intersect[@tailcall]) rest s2
    ;;
intersect [1;3;5;7] [1;5;3;4;2];;    

let union s1 s2 =
  let rec i_union s res =
    match s with
    [] -> res
    | (a::rest) when mem a res -> i_union rest res
    | (a::rest) -> i_union rest (a::res)
  in
    i_union (s1 @ s2) []
    ;;
union [1;2;3;4;5] [1;3;5;6;7];;

let rec diff s1 s2 =
  match s1 with
  [] -> []
  | (a::rest) when mem a s2 -> diff rest s2
  | (a::rest) -> a :: (diff rest s2)
  ;;
diff [2;1;3;4;5] [1;3;7];;
```

### 5.4
```
let rec map f = function
  [] -> []
  | x :: rest -> f x :: map f rest
  ;;

let f = (+) 1;;
let g = ( * ) 2;;
let l = [1;2;3;4;5];;
map f (map g l);;

map (fun a -> f( g a)) l;; 
```

### 5.5
```
let rec fold_right f l e = match l with
[] -> e
| x :: rest -> f x (fold_right f rest e)
;;

let concat n = fold_right (@) n [];;
concat [[0; 3; 4]; [2]; []; [5; 0]];;

let forall f x = fold_right (fun a -> (&&) (f a)) x true;;
forall (fun x -> x >= 5) [9;20;5];;

let exists f x = fold_right (fun a -> (||) (f a)) x false;;
exists (fun x -> (x mod 7) = 0) [23; -98; 19; 53];;
```

```
let rec quick_sort lst results =
  match lst with 
  [] -> results
  | [a] -> a::results
  | pivot :: rest ->
      let rec partition left right lst results =
        match lst with
        [] -> quick_sort left  (pivot :: (quick_sort right results))
        | y :: ys ->
            if pivot < y then
              partition left (y :: right) ys results
            else
              partition (y :: left) right ys results
      in partition [] [] rest results;;
```

### 5.7

```

```

### 5.8
```
let rec map f = function
  [] -> []
  | x :: rest -> f x :: map f rest
  ;;
  
let map2 f n =
  let rec i_map2 f n res =
    match n with
    [] -> res
    | x :: rest -> (i_map2[@tailcall]) f rest (f(x)::res)
  in i_map2 f n []
  ;;

let rec fold_left f e l =
  match l with
      [] -> e
    | x :: rest -> fold_left f (f e x) rest;;

let map2 f xs =
  let results = fold_left (fun x y -> (f y)::x) [] xs
  in
  fold_left (fun x y -> y::x) [] results;;
```
