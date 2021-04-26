### 9.1
https://github.com/kaznum/programming_in_ocaml_exercise/blob/master/ex9.1/newton.ml

```
open Num;;

let deriv f =
  let dx = 0.1e-10 in
    fun x -> (f(x +. dx) -. f(x)) /. dx
    ;;

let fixpoint f init = (* fの不動点，すなわちf(r)=rなるrを求める *)
  let threshold = 0.1e-10 in
  let rec loop x =
    let next = f x in
    if abs_float (x -. next) < threshold then
      x
    else
      loop next
    in loop init
    ;;
let newton_transform f = fun x -> x -. f(x) /. (deriv f x);;
let newton_method f guess = fixpoint (newton_transform f) guess;;

```

###  9.2

```
module type TABLE2 =
  sig
    type ('a, 'b) t
    val empty : ('a, 'b) t
    val add : 'a -> 'b -> ('a, 'b) t -> ('a, 'b) t
    val retrieve : 'a -> ('a, 'b) t -> 'b option
    val dump : ('a, 'b) t -> ('a * 'b) list
  end
;;

module Tree : TABLE2 =
struct
  type ('a, 'b) t = Lf | Br of ('a * 'b) * ('a, 'b) t * ('a, 'b) t

  let empty = Lf

  let rec add key datum tree =
    match tree with
    Lf -> Br((key, datum), Lf, Lf)
    | (Br((x,y), left, right)) when x = key -> Br((key,datum), left, right)
    | (Br((x,y), left, right)) when key < x -> Br((x, y), (add key datum left), right)
    | (Br((x,y), left, right))              -> Br((x, y), left, (add key datum right))
    
  let rec retrieve key tree =
    match tree with
    Lf -> None
    | (Br((x,y), left, right)) when x = key -> Some y
    | (Br((x,y), left, right)) when key < x -> retrieve key left
    | (Br((x,y), left, right))              -> retrieve key right

  let rec dump tree =
    match tree with
    Lf -> []
    | (Br((x, y), left, right)) -> [(x, y)] @ (dump left) @ (dump right)

end;;

let ( <<< ) tree (key, value) = Tree.add key value tree;;
let tree = Tree.empty
  <<< (1, "a1")
  <<< (3, "a3")
  <<< (5, "a5")
  <<< (2, "a2")
  <<< (9, "a9")
  <<< (8, "a8")
  <<< (10, "a10")
  <<< (7, "a7")
  <<< (1, "xxx")
  <<< (6, "a6");;
Tree.dump tree;;
Tree.retrieve 1 tree;;
Tree.retrieve 9 tree;;
Tree.retrieve 15 tree;;
```

### 9.3

```
module type QUEUE =
sig
  type 'a t
  exception Empty
  val empty: 'a t
  val add: 'a t -> 'a -> 'a t
  val take: 'a t -> 'a * 'a t
  val peek: 'a t -> 'a
end;;

module Queue1 : QUEUE =
struct
  type 'a t = 'a list

  exception Empty

  let empty = []

  let add q a = q @ [a]
  
  let take q =
     match q with
     [] -> raise Empty
     | x::rest -> (x, rest)

  let peek q =
     match q with
     [] -> raise Empty
     | x :: _ -> x
end;;
  
module Queue2 : QUEUE =
struct
  type 'a t = Queue of ('a list * 'a list)
  
  exception Empty

  let empty = Queue([], [])
  
  let peek = function
    Queue ([], _) -> raise Empty
    | Queue (x :: _, _) -> x

  let add q a =
    match q with
    Queue ([], _) -> Queue([a], [])
    | Queue (first, second) -> Queue (first, a::second)

  let take q =
    match q with
    Queue ([], _) -> raise Empty
    | Queue (x::[], y) -> (x, Queue ((List.fold_left (fun ts t -> t::ts) [] y), []))
    | Queue (x::xrest, y) -> (x, Queue (xrest, y))

end;;
```
