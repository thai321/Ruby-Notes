# Ruby-Note

- [Enumerable](#Enumerable)
  - [all?](#all?)
  - [any?](#all?)
  - [chunk](#chunk)
  - [chunk_while?](#chunk-while)
  - [collect](#collect)
  - [collect_concat](#collect_concat)
  - [count](#count)
  - [cycle](#cycle)
  - [detect](#detect)
  - [drop](#drop)
  - [drop_while](#drop_while)
  - [each_cons](#each_cons)
  - [each_entry](#each_entry)
  - [each_slice](#each_slice)



<a name="Enumerable"></a>
## Enumerable
<a name="all?"></a>
### all? , any? --> true or false
```rb
%w[ant bear cat].all? { |word| word.length >= 3 }
%w[ant bear cat].any? { |word| word.length >= 3 } #=> true
```

-------
<a name="chunk"></a>
### chunk --> → an_enumerator
```rb
arrChunks = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5].chunk { |n| n.even?}
arrChunks.each {|bool, arr| puts [bool, arr] }
```

---------
<a name="chunk-while"></a>
### chunk_while {|before, after| bool } --> an_enumerator

```rb
a = [1,2,4,9,10,11,12,15,16,19,20,21]
b = a.chunk_while {|i, j| i+1 == j }
p b.to_a #=> [[1, 2], [4], [9, 10, 11, 12], [15, 16], [19, 20, 21]]
c = b.map {|a| a.length < 3 ? a : "#{a.first}-#{a.last}" }
p c #=> [[1, 2], [4], "9-12", [15, 16], "19-21"]
d = c.join(",")
p d #=> "1,2,4,9-12,15,16,19-21"
```

```rb
a = [0, 9, 2, 2, 3, 2, 7, 5, 9, 5]
p a.chunk_while {|i, j| i <= j }.to_a
#=> [[0, 9], [2, 2, 3], [2, 7], [5, 9], [5]]
```

Take me there

```rb
a = [7, 5, 9, 2, 0, 7, 9, 4, 2, 0]
p a.chunk_while {|i, j| i.even? == j.even? }.to_a
#=> [[7, 5, 9], [2, 0], [7, 9], [4, 2, 0]]
```


-------
<a name="collect"></a>
### collect { |obj| block } → array
### collect → an_enumerator

```rb
(1..4).map { |i| i*i }      #=> [1, 4, 9, 16]
(1..4).collect { "cat"  }   #=> ["cat", "cat", "cat", "cat"]
```

----
<a name="collect_concat"></a>
### collect_concat { |obj| block } → array
### collect_concat → an_enumerator

```rb
[1, 2, 3, 4].flat_map { |e| [e, -e] } #=> [1, -1, 2, -2, 3, -3, 4, -4]
[[1, 2], [3, 4]].flat_map { |e| e + [100] } #=> [1, 2, 100, 3, 4, 100]
```


-----
<a name="count"></a>
### count → int
### count(item) → int
### count { |obj| block } → int

```rb
ary = [1, 2, 4, 2]
ary.count               #=> 4
ary.count(2)            #=> 2
ary.count{ |x| x%2==0 } #=> 3
```

------
<a name="cycle"></a>
### cycle(n=nil) { |obj| block } → nil
### cycle(n=nil) → an_enumerator

```rb
a = ["a", "b", "c"]
a.cycle { |x| puts x }  # print, a, b, c, a, b, c,.. forever.
a.cycle(2) { |x| puts x }  # print, a, b, c, a, b, c.
```


-----
<a name="detect"></a>
### detect(ifnone = nil) { |obj| block } → obj or nil
### detect(ifnone = nil) → an_enumerator

```rb
(1..100).detect  => #<Enumerator: 1..100:detect>
(1..100).find    => #<Enumerator: 1..100:find>

(1..10).detect   { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..10).find     { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..100).detect  { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35
(1..100).find    { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35
```

-----
<a name="drop"></a>
### drop(n) → array

```rb
a = [1, 2, 3, 4, 5, 0]
a.drop(3)             #=> [4, 5, 0]
```


-------
<a name="drop_while"></a>
### drop_while { |obj| block } → array click to toggle source
### drop_while → an_enumerator

- Drops elements up to, but not including, the first element for which the block returns nil or false and returns an array containing the remaining elements.

- If no block is given, an enumerator is returned instead.


```rb
a = [1, 2, 3, 4, 5, 0]
a.drop_while { |i| i < 3 }   #=> [3, 4, 5, 0]
```

------
<a name="each_cons"></a>
### each_cons(n) { ... } → nil click to toggle source
### each_cons(n) → an_enumerator

- Iterates the given block for each array of consecutive <n> elements. If no block is given, returns an enumerator.

```rb
(1..10).each_cons(3) { |a| p a }
# outputs below
[1, 2, 3]
[2, 3, 4]
[3, 4, 5]
[4, 5, 6]
[5, 6, 7]
[6, 7, 8]
[7, 8, 9]
[8, 9, 10]
```

------
<a name="each_entry"></a>
### each_entry { |obj| block } → enum click to toggle source
### each_entry → an_enumerator
- Calls block once for each element in self, passing that element as a parameter, converting multiple values from yield to an array.

- If no block is given, an enumerator is returned instead.


```rb
class Foo
  include Enumerable
  def each
    yield 1
    yield 1, 2
    yield
  end
end
Foo.new.each_entry{ |o| p o }

# product
1
[1, 2]
nil
```

------
<a name="each_slice"></a>
### each_slice(n) { ... } → nil
### each_slice(n) → an_enumerator

```rb
(1..10).each_slice(3) { |a| p a }
# outputs below
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
[10]
```
