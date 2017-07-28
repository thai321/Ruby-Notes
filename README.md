# Ruby-Note

- [Enumerable](#Enumerable)
  - [all?](#all?)
  - [any?](#all?)
  - [chunk](#chunk)
  - [chunk_while?](#chunk_while)
  - [any?](#all?)
  - [any?](#all?)



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
