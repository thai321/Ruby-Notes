# Ruby-Note

- [Enumerable](#Enumerable)
  - [all?](#all?)
  - [any?](#all?)
  - [chunk](#chunk)
  - [chunk_while?](#chunk-while)
  - [collect](#collect)
  - [collect_concat](#collect_concat)
  - [count](#count)



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
### count → int click to toggle source
### count(item) → int
### count { |obj| block } → int

```rb
ary = [1, 2, 4, 2]
ary.count               #=> 4
ary.count(2)            #=> 2
ary.count{ |x| x%2==0 } #=> 3
```
