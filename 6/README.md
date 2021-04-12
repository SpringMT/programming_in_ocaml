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
```
