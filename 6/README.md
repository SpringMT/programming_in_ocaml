### 6.1

```
type figure = Point
  | Circle of int
  | Rectangle of int * int
  | Square of int;;

let similar x y =
  match (x, y) with
    (Point, Point) | (Circle _, Circle _) | (Square _, Square _) -> true
    | (Rectangle (l1, l2), Rectangle (l3, l4)) -> (l3 * l2 - l4 * l1) = 0
    | _ -> false;;


let similar2 x y =
  match (x, y) with
    (Point, Point) | (Circle _, Circle _) | (Square _, Square _) -> true
    | (Rectangle (l1, l2), Rectangle (l3, l4)) -> (l3 * l2 - l4 * l1) = 0
    | (Rectangle (l1, l2), Square _) -> l1 = l2
    | (Square _, Rectangle (l1, l2)) -> l1 = l2
    | _ -> false;;

similar (Rectangle (4, 4)) (Square (2));;
similar2 (Rectangle (4, 4)) (Square (2));;
```

### 6.2

```
type figure = Point
  | Circle of int
  | Rectangle of int * int
  | Square of int;;

type 'a with_location = {loc_x: float; loc_y: float; body: 'a};;

let square a = a *. a;;

let overlap_circle x1 y1 r1 x2 y2 r2 =
  square(x2 -. x1) +. square(y2 -. y1) < square(r2 +. r1)
  ;;

let overlap f1 f2 =
  match f1.body, f2.body with
	  | Circle r1, Circle r2 -> overlap_circle f1.loc_x f1.loc_y (float_of_int r1) f2.loc_x f2.loc_y (float_of_int r2)
    ;;
  
overlap {loc_x = 3.0; loc_y = 1.0; body = Circle 1} {loc_x = 0.0; loc_y = 1.0; body = Circle 1};;
overlap {loc_x = 3.0; loc_y = 1.0; body = Circle 2} {loc_x = 0.0; loc_y = 1.0; body = Circle 1};;
overlap {loc_x = 3.0; loc_y = 1.0; body = Circle 2} {loc_x = 0.1; loc_y = 1.0; body = Circle 1};;
```
https://ymotongpoo.hatenablog.com/entry/20100414/1271204764

### 6.3

```
type nat = Zero | OneMoreThan of nat;;
let rec add m n =
  match m with
  Zero -> n
  | OneMoreThan m' -> OneMoreThan (add m' n)
  ;;

let rec mul m n = 
  match (m, n) with
    (Zero, _) | (_, Zero) -> Zero
  | (OneMoreThan Zero, _) -> n
  | (OneMoreThan a, _) -> add (mul a n) n
  ;;

let zero = Zero
and two = OneMoreThan (OneMoreThan Zero)
and three = OneMoreThan (OneMoreThan (OneMoreThan Zero))
;;
mul three two;;

let rec monus m n =
  match (m, n) with
  (Zero, _) -> Zero
  | (_, Zero) -> m
  | OneMoreThan a, OneMoreThan b -> monus a b
  ;;
monus three two;;

let rec minus m n =
  match (m, n) with
  (Zero, _) -> None
  | (_, Zero) -> Some m
  | OneMoreThan a, OneMoreThan b -> minus a b
  ;;
  
minus three two;;
```

### 6.5
```
type 'a tree =
  Lf
  | Br of 'a * 'a tree * 'a tree;;
let rec comptree x n =
  match n with
  0 -> Lf
  | _ -> Br(x, (comptree x (n-1)), (comptree x (n-1)))
  ;;

let comptree' n =
  let rec comptree_i n' i =
    match n' with
    0 -> Lf
    | _ -> Br(i, (comptree_i (n'-1) (2*i+1)), (comptree_i (n'-1) (2*i)))
  in
    comptree_i n 1
  ;;
comptree' 3;;
```
