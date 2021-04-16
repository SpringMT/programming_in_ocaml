### 8.2

```
let incr n = 
  n := !n + 1
  ;;
let x = ref 3;;
incr x;;
!x;;
```

### 8.4

```
let rec fib n =
  match n with
  0 -> 0
  | 1 -> 1
  | _ -> fib(n - 1) + fib(n - 2)
  ;;

let fib2 n=
  let rec fib_pair n =
    if n = 1 then
      (1, 0)
    else
      let (i, j) = fib_pair (n - 1) in
      (i + j, i)
  in
    let (i, _) = fib_pair n in i
  ;;

let fib3 n =
  let prev = ref 0 and current = ref 1 and next = ref 1 and i = ref 1 in
  while (n > !i) do
    next := !current + !prev;
    prev := !current;
    current := !next;
    i := !i + 1;
  done;
  !current
;;
fib 10;;
fib3 10;;
```
