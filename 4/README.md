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



