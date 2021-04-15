### 7.1

```
let find x n =
  let rec find_ex x' n' =
    match n' with
    [] -> raise Not_found
    | a :: l when a = x' -> 1
    | _ :: l -> 1 + find_ex x' l
  in try Some (find_ex x n) with
    Not_found -> None
;;
```

### 7.2

```
let rec prod_list n =
  match n with
  [] -> 1
  | a::rest when a = 0 ->  raise (Invalid_argument "include zero in n")
  | a::rest -> a * prod_list rest
;;
prod_list [1; 2; 3;];;
prod_list [1; 2; 0;];;
```
