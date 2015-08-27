
# Haskell

- file:///Library/Haskell/doc/start.html


## Links
- http://learnyouahaskell.com/chapters
- http://www.haskell.org/haskellwiki/Learning_Haskell
- http://book.realworldhaskell.org/read/
- http://lisperati.com/haskell/
- http://shuklan.com/haskell/index.html
- http://haskelllive.com
- http://tryhaskell.org/
- [Haskell Platform](http://hackage.haskell.org/platform/)
- [Leksah IDE](http://leksah.org/download.html)

***
Learn You A Haskell
====

Introduction
----
- Haskell is a purely functional programming language.
- Haskell is lazy. 
- Haskell is statically typed.
- Haskell uses a very good type system that has type inference.

Starting Out
----
```
:set prompt "ghci> "
```

/= is operator for not equal.

In Haskell, functions are called by writing the function name, a space and then the parameters, separated by spaces.

If a function takes two parameters, we can also call it as an infix function by surrounding it with backticks. For instance, the div function takes two integers and does integral division between them. Doing div 92 10 results in a 9. But when we call it like that, there may be some confusion as to which number is doing the division and which one is being divided. So we can call it as an infix function by doing 92 \`div` 10 and suddenly it's much clearer.

Functions are defined in a similar way that they are called. The function name is followed by parameters seperated by spaces. But when defining functions, there's a = and after that we define what the function does.

```
doubleMe x = x + x 

doubleUs x y = x*2 + y*2 

doubleUs x y = doubleMe x + doubleMe y   

doubleSmallNumber x = if x > 100  
                        then x  
                        else x*2 
                        
doubleSmallNumber' x = (if x > 100 then x else x*2) + 1 
```
We usually use ' to either denote a strict version of a function (one that isn't lazy) or a slightly modified version of a function or a variable.

### Lists
In Haskell, lists are a homogenous data structure. It stores several elements of the same type. Lists are denoted by square brackets and the values in the lists are separated by commas.

> Note: We can use the let keyword to define a name right in GHCI. Doing let a = 1 inside GHCI is  the equivalent of writing a = 1 in a script and then loading it.

```
let lostNumbers = [4,8,15,16,23,42] 
```

A common task is putting two lists together. This is done by using the ++ operator.
```
"hello" ++ " " ++ "world"
```

Haskell has to walk through the whole list on the left side of ++. That's not a problem when dealing with lists that aren't too big. But putting something at the end of a list that's fifty million entries long is going to take a while. However, putting something at the beginning of a list using the : operator (also called the cons operator) is instantaneous.

```
'A':" SMALL CAT" 
5:[1,2,3,4,5]
```

>Note: [], [[]] and[[],[],[]] are all different things. The first one is an empty list, the seconds one is a list that contains one empty list, the third one is a list that contains three empty lists.

To get an element out of a list by index, use !!. The indices start at 0.

```
ghci> "Steve Buscemi" !! 6  
'B' 

ghci> [3,2,1] > [2,1,0]  
True  

ghci> head [5,4,3,2,1]  
5  
ghci> tail [5,4,3,2,1]  
[4,3,2,1]   
ghci> tail [5,4,3,2,1]  
[4,3,2,1]   
ghci> init [5,4,3,2,1]  
[5,4,3,2] 
ghci> length [5,4,3,2,1]  
5  
ghci> reverse [5,4,3,2,1]  
[1,2,3,4,5]  
ghci> take 3 [5,4,3,2,1]  
[5,4,3]
ghci> drop 3 [8,4,2,1,5,6]  
[1,5,6] 
ghci> minimum [8,4,2,1,5,6]  
1  
ghci> maximum [1,9,2,3,4]  
9   
ghci> sum [5,2,1,6,3,2,5,7]  
31  
ghci> product [6,2,1,2]  
24 
```
elem takes a thing and a list of things and tells us if that thing is an element of the list.
```
ghci> 4 `elem` [3,4,5,6]  
True  
ghci> 10 `elem` [3,4,5,6]  
False 
```

#### Ranges
```
ghci> [1..20]  
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]  
ghci> ['a'..'z']  
"abcdefghijklmnopqrstuvwxyz"  
ghci> ['K'..'Z']  
"KLMNOPQRSTUVWXYZ"  
```
You can also specify a step:
```
ghci> [2,4..20]  
[2,4,6,8,10,12,14,16,18,20]  
ghci> [3,6..20]  
[3,6,9,12,15,18] 
```
To make a list with all the numbers from 20 to 1, you can't just do [20..1], you have to do [20,19..1].

### List Comprehensions
- The part before the pipe is called the output function.
- After the pipe is the variable, and the input set.
- Predicate comes after a comma.

```
ghci> [x*2 | x <- [1..10], x*2 >= 12]  
[12,14,16,18,20]  

ghci> [x*2 | x <- [1..10]]  
[2,4,6,8,10,12,14,16,18,20] 

ghci> [ x | x <- [50..100], x `mod` 7 == 3]  
[52,59,66,73,80,87,94]  

boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x] 
ghci> boomBangs [7..13]  
["BOOM!","BOOM!","BANG!","BANG!"] 

ghci> [ x | x <- [10..20], x /= 13, x /= 15, x /= 19]  
[10,11,12,14,16,17,18,20]  
```

### Tuples
Unlike a list, a tuple can contain a combination of several types.

Use tuples when you know in advance how many components some piece of data should have. Tuples are much more rigid because each different size of tuple is its own type, so you can't write a general function to append an element to a tuple â€” you'd have to write a function for appending to a pair, one function for appending to a triple, one function for appending to a 4-tuple, etc.

Two useful functions that operate on pairs:
```
ghci> fst (8,11)  
8  
ghci> fst ("Wow", False)  
"Wow" 
ghci> snd (8,11)  
11  
ghci> snd ("Wow", False)  
False  
```

A cool function that produces a list of pairs: zip. It takes two lists and then zips them together into one list by joining the matching elements into pairs.
```
ghci> zip [1,2,3,4,5] [5,5,5,5,5]  
[(1,5),(2,5),(3,5),(4,5),(5,5)]  
ghci> zip [1 .. 5] ["one", "two", "three", "four", "five"]  
[(1,"one"),(2,"two"),(3,"three"),(4,"four"),(5,"five")] 
ghci> zip [1..] ["apple", "orange", "cherry", "mango"]  
[(1,"apple"),(2,"orange"),(3,"cherry"),(4,"mango")]  
```

Types and Typeclasses
----
Everything in Haskell has a type, so the compiler can reason quite a lot about your program before compiling it.

:t command which, followed by any valid expression, tells us its type.

Functions also have types. When writing our own functions, we can choose to give them an explicit type declaration.

The [Char] type is synonymous with String.

Here's a simple function that takes three integers and adds them together:
```
addThree :: Int -> Int -> Int -> Int  
addThree x y z = x + y + z  
```

The parameters are separated with -> and there's no special distinction between the parameters and the return type. The return type is the last item in the declaration and the parameters are the first three. 

Common types: Int, Integer (not bounded, can represent really bug numbers), Float, Double, Bool, Char, String.

Tuples are types but they are dependent on their length as well as the types of their components.

### Type variables
This is much like generics in other languages, only in Haskell it's much more powerful because it allows us to easily write very general functions if they don't use any specific behavior of the types in them. Functions that have type variables are called polymorphic functions. The type declaration of head states that it takes a list of any type and returns one element of that type.
```
ghci> :t head  
head :: [a] -> a  
```

### Typeclasses 101
A typeclass is a sort of interface that defines some behavior. If a type is a part of a typeclass, that means that it supports and implements the behavior the typeclass describes.

```
ghci> :t (==)  
(==) :: (Eq a) => a -> a -> Bool  
```
Everything before the => symbol is called a class constraint. We can read the previous type declaration like this: the equality function takes any two values that are of the same type and returns a Bool. The type of those two values must be a member of the Eq class (this was the class constraint).

- Eq is used for types that support equality testing.
- Ord is for types that have an ordering.
- Ordering is a type that can be GT, LT or EQ, meaning greater than, lesser than and equal, respectively.
- Members of Show can be presented as strings.
- Read is sort of the opposite typeclass of Show. The read function takes a string and returns a type which is a member of Read.
 - Type annotations are a way of explicitly saying what the type of an expression should be. We do that by adding :: at the end of the expression and then specifying a type.
- Enum members are sequentially ordered types — they can be enumerated. 
- Bounded members have an upper and a lower bound.
- Num is a numeric typeclass. Its members have the property of being able to act like numbers.
- Integral is also a numeric typeclass. 
- Floating includes only floating point numbers, so Float and Double.


Syntax in Functions
----

### Pattern matching
- Variable binding, pattern deconstructing
- Functions
- Tuples
- List comprehensions
- as patterns

### Guards, guards!
```
bmiTell :: (RealFloat a) => a -> a -> String  
bmiTell weight height  
    | weight / height ^ 2 <= 18.5 = "You're underweight, you emo, you!"  
    | weight / height ^ 2 <= 25.0 = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | weight / height ^ 2 <= 30.0 = "You're fat! Lose some weight, fatty!"  
    | otherwise                 = "You're a whale, congratulations!"  
```
```
myCompare :: (Ord a) => a -> a -> Ordering  
a `myCompare` b  
    | a > b     = GT  
    | a == b    = EQ  
    | otherwise = LT 
```
### Where!?
```
bmiTell :: (RealFloat a) => a -> a -> String  
bmiTell weight height  
    | bmi <= skinny = "You're underweight, you emo, you!"  
    | bmi <= normal = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= fat    = "You're fat! Lose some weight, fatty!"  
    | otherwise     = "You're a whale, congratulations!"  
    where bmi = weight / height ^ 2  
          (skinny, normal, fat) = (18.5, 25.0, 30.0)   
```
```
calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi w h | (w, h) <- xs]  
    where bmi weight height = weight / height ^ 2 
```
 
### Let it be
```
cylinder :: (RealFloat a) => a -> a -> a  
cylinder r h = 
    let sideArea = 2 * pi * r * h  
        topArea = pi * r ^2  
    in  sideArea + 2 * topArea  
```
```
ghci> [let square x = x * x in (square 5, square 3, square 2)]  
[(25,9,4)]  
```
```
calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi | (w, h) <- xs, let bmi = w / h ^ 2]  
```

### Case expressions
```
describeList :: [a] -> String  
describeList xs = "The list is " ++ case xs of [] -> "empty."  
                                               [x] -> "a singleton list."   
                                               xs -> "a longer list."  
```

Recursion
----
```
maximum' :: (Ord a) => [a] -> a  
maximum' [] = error "maximum of empty list"  
maximum' [x] = x  
maximum' (x:xs)   
    | x > maxTail = x  
    | otherwise = maxTail  
    where maxTail = maximum' xs  
```
An even clearer way to write this function is to use max.
```
maximum' :: (Ord a) => [a] -> a  
maximum' [] = error "maximum of empty list"  
maximum' [x] = x  
maximum' (x:xs) = max x (maximum' xs)  
```

```
quicksort :: (Ord a) => [a] -> [a]  
quicksort [] = []  
quicksort (x:xs) =   
    let smallerSorted = quicksort [a | a <- xs, a <= x]  
        biggerSorted = quicksort [a | a <- xs, a > x]  
    in  smallerSorted ++ [x] ++ biggerSorted  
```
Higher order functions
----
Haskell functions can take functions as parameters and return functions as return values. A function that does either of those is called a higher order function. 
### Curried functions
- Every function in Haskell officially only takes one parameter.
- Putting a space between two things is simply **function application**. The space is sort of like an operator and it has the highest precedence.
- If we call a function with too few parameters, we get back a **partially applied** function, meaning a function that takes as many parameters as we left out.
- Infix functions can also be partially applied by using sections. To section an infix function, simply surround it with parentheses and only supply a parameter on one side.
- The only special thing about sections is using -.

### Higher order functions
```
zipWith' :: (a -> b -> c) -> [a] -> [b] -> [c]  
zipWith' _ [] _ = []  
zipWith' _ _ [] = []  
zipWith' f (x:xs) (y:ys) = f x y : zipWith' f xs ys  
```
### Maps and filters
```
ghci> map (+3) [1,5,3,1,6]  
[4,8,6,4,9]  
ghci> map (++ "!") ["BIFF", "BANG", "POW"]  
["BIFF!","BANG!","POW!"]  
ghci> map (replicate 3) [3..6]  
[[3,3,3],[4,4,4],[5,5,5],[6,6,6]]  
ghci> map (map (^2)) [[1,2],[3,4,5,6],[7,8]]  
[[1,4],[9,16,25,36],[49,64]]  
ghci> map fst [(1,2),(3,5),(6,3),(2,6),(2,5)]  
[1,3,6,2,2] 
```
Each of these could be achieved with a list comprehension. map (+3) [1,5,3,1,6] is the same as writing [x+3 | x <- [1,5,3,1,6]]. However, using map is much more readable for cases where you only apply some function to the elements of a list.

```
ghci> filter (>3) [1,5,3,2,1,6,4,3,2,1]  
[5,6,4]  
ghci> filter (==3) [1,2,3,4,5]  
[3]  
ghci> filter even [1..10]  
[2,4,6,8,10]  
ghci> let notNull x = not (null x) in filter notNull [[1,2,3],[],[3,4,5],[2,2],[],[],[]]  
[[1,2,3],[3,4,5],[2,2]]  
ghci> filter (`elem` ['a'..'z']) "u LaUgH aT mE BeCaUsE I aM diFfeRent"  
"uagameasadifeent" 
```
All of this could also be achived with list comprehensions by the use of predicates. There's no set rule for when to use map and filter versus using list comprehension.

```
quicksort :: (Ord a) => [a] -> [a]    
quicksort [] = []    
quicksort (x:xs) =     
    let smallerSorted = quicksort (filter (<=x) xs)  
        biggerSorted = quicksort (filter (>x) xs)   
    in  smallerSorted ++ [x] ++ biggerSorted 
```

### Lambdas
Lambdas are basically anonymous functions that are used because we need some functions only once. Normally, we make a lambda with the sole purpose of passing it to a higher-order function. To make a lambda, we write a \ and then we write the parameters, separated by spaces. After that comes a -> and then the function body. We usually surround them by parentheses, because otherwise they extend all the way to the right.
```
ghci> zipWith (\a b -> (a * 30 + 3) / b) [5,4,3,2,1] [1,2,3,4,5]  
[153.0,61.5,31.0,15.75,6.6]  

ghci> map (\(a,b) -> a + b) [(1,2),(3,5),(6,3),(2,6),(2,5)]  
[3,8,9,8,7] 
```

### folds
They're sort of like the map function, only they reduce the list to some single value.

 - foldl
 - foldr
 - foldl1
 - foldr1
 - scanl
 - scanr

### Function application with $

Normal function application (putting a space between two things) has a really high precedence, the \$ function has the lowest precedence. Function application with a space is left-associative, function application with \$ is right-associative.

Consider the expression `sum (map sqrt [1..130])`. Because \$ has such a low precedence, we can rewrite that expression as `sum $ map sqrt [1..130]`.

Can rewrite `sum (filter (> 10) (map (*2) [2..10]))` as `sum $ filter (> 10) $ map (*2) [2..10]`.

But apart from getting rid of parentheses, $ means that function application can be treated just like another function. That way, we can, for instance, map function application over a list of functions.

```
ghci> map ($ 3) [(4+), (10*), (^2), sqrt]  
[7.0,30.0,9.0,1.7320508075688772]  
```

### Function composition
We do function composition with the . function.

Can use lambdas, but many times, function composition is clearer and more concise.

```
ghci> map (\x -> negate (abs x)) [5,-3,-6,7,-3,2,-19,24]  
[-5,-3,-6,-7,-3,-2,-19,-24]  

ghci> map (negate . abs) [5,-3,-6,7,-3,2,-19,24]  
[-5,-3,-6,-7,-3,-2,-19,-24]  

ghci> map (\xs -> negate (sum (tail xs))) [[1..5],[3..6],[1..7]]  
[-14,-15,-27]  

ghci> map (negate . sum . tail) [[1..5],[3..6],[1..7]]  
[-14,-15,-27]  
```

But what about functions that take several parameters? Well, if we want to use them in function composition, we usually have to partially apply them just so much that each function takes just one parameter. `sum (replicate 5 (max 6.7 8.9))` can be rewritten as `(sum . replicate 5 . max 6.7) 8.9` or as `sum . replicate 5 . max 6.7 $ 8.9`. What goes on in here is this: a function that takes what max 6.7 takes and applies replicate 5 to it is created. Then, a function that takes the result of that and does a sum of it is created. Finally, that function is called with 8.9. But normally, you just read that as: apply 8.9 to max 6.7, then apply replicate 5 to that and then apply sum to that. If you want to rewrite an expression with a lot of parentheses by using function composition, you can start by putting the last parameter of the innermost function after a \$ and then just composing all the other function calls, writing them without their last parameter and putting dots between them. If you have `replicate 100 (product (map (*3) (zipWith max [1,2,3,4,5] [4,5,6,7,8])))`, you can write it as `replicate 100 . product . map (*3) . zipWith max [1,2,3,4,5] $ [4,5,6,7,8]`. If the expression ends with three parentheses, chances are that if you translate it into function composition, it'll have three composition operators.

Another common use of function composition is defining functions in the so-called point free style.

```
sum' :: (Num a) => [a] -> a     
sum' xs = foldl (+) 0 xs     
```

The xs is exposed on both right sides. Because of currying, we can omit the xs on both sides, because calling foldl (+) 0 creates a function that takes a list. Writing the function as sum' = foldl (+) 0 is called writing it in point free style.



Modules
----
A Haskell module is a collection of related functions, types and typeclasses. A Haskell program is a collection of modules where the main module loads up the other modules and then uses the functions defined in them to do something.

The Prelude module is imported by default.

The syntax for importing modules in a Haskell script is import <module name>. This must be done before defining any functions, so imports are usually done at the top of the file.
