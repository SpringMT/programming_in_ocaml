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
