## 練習問題

### 4.1
```
let uncurry f (x, y) = f x y;;
```

### 4.2
```

let rec repeat f n x =
      if n > 0 then repeat f (n - 1) (f x) else x;;
val repeat : ('a -> 'a) -> int -> 'a -> 'a = <fun>

let fib n =
  let (fibn, _) = repeat (fun (i, j) -> ((i + j), i)) n (1, 0)
    in fibn;;

```

