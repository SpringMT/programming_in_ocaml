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

### 8.9
```
type 'a mlist = MNil | MCons of 'a * 'a mlist ref;;
type 'a queue = {mutable head : 'a mlist; mutable tail : 'a mlist};;
let create () = {head = MNil; tail = MNil};;
let add a = function
  {head = MNil; tail = MNil} as q ->
    let c = MCons (a, ref MNil) in
    q.head <- c; q.tail <-c
  | {tail = MCons(_, next)} as q ->
    let c = MCons (a, ref MNil) in
    next := c; q.tail <- c
  | _ -> failwith "enqueue: input queue broken"
  ;;

let peek = function
  {head = MNil; tail = MNil} -> failwith "hd: queue is empty"
  | {head = MCons(a, _)} -> a
  | _ -> failwith "hd: queue is broken"
  ;;
  
let take = function
  {head = MNil; tail = MNil} -> failwith "dequeue: queue is empty"
  | {head = MCons(a, next)} as q ->
    q.head <- !next;
    if !next = MNil then
      q.tail <- MNil;
    a
  | _ -> failwith "dequeue: queue is broken"
  ;;

let q : int queue = create();;
add 1 q; add 2 q;add 3 q;;
q;;
peek q;;

take q;;
ignore(take q); add 5 q; peek q;;
```

### 8.10

```
let print_int n = 
  output_string stdout (string_of_int n)
  ;;
```


### 8.11

```
let display_file file =
  let input = open_in file in
  let line_num = ref 1 in
  try
    while true do
      output_string stdout ((string_of_int !line_num) ^ " " ^ (input_line input) ^ "\n");
      line_num := !line_num + 1;
    done
  with End_of_file -> ();
  close_in input
  ;;
```

### 8.12

```
let cp src dst =
  let src_fd = open_in src and dst_fd = open_out dst in
  try
    while true do
      output_string dst_fd ((input_line src_fd) ^ "\n");
    done
  with End_of_file -> ();
  close_in src_fd;
  close_out dst_fd;
;;
```

