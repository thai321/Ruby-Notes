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
  - [each_with_index](#each_with_index)
  - [each_with_object](#each_with_object)
  - [entries](#entries)
  - [find](#find)
  - [find_all](#find_all)
  - [find_index](#find_index)
  - [first](#first)
  - [flat_map](#flat_map)
  - [grep](#grep)
  - [grep_v](#grep_v)
  - [group_by](#group_by)
  - [include?](#include?)
  - [inject](#inject)
  - [lazy](#lazy)
  - [map](#map)
  - [max](#max)
  - [max_by](#max_by)
  - [member?](#member?)
  - [min](#min)
  - [min_by](#min_by)
  - [minmax](#minmax)
  - [minmax_by](#minmax_by)
  - [none?](#none?)
  - [one?](#one?)
  - [partition](#partition)
  - [reduce](#reduce)
  - [reject](#reject) also see [find_all](#find_all)
  - [reverse_each](#reverse_each)
  - [select](#select) also see [reject](#reject)




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

------
<a name="each_with_index"></a>
### each_with_index(*args) { |obj, i| block } → enum
### each_with_index(*args) → an_enumerator

- Calls block with two arguments, the item and its index, for each item in enum. Given arguments are passed through to each().

- If no block is given, an enumerator is returned instead.

```rb
hash = Hash.new
%w(cat dog wombat).each_with_index { |item, index|
  hash[item] = index
}
hash   #=> {"cat"=>0, "dog"=>1, "wombat"=>2}
```


-------
<a name="each_with_object"></a>
### each_with_object(obj) { |(*args), memo_obj| ... } → obj
### each_with_object(obj) → an_enumerator

- Iterates the given block for each element with an arbitrary object given, and returns the initially given object.

- If no block is given, returns an enumerator.
```rb
evens = (1..10).each_with_object([]) { |i, a| a << i*2 }
#=> [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```


------
<a name="entries"></a>
### entries(*args) → array
- Returns an array containing the items in enum.

```rb
(1..7).to_a                       #=> [1, 2, 3, 4, 5, 6, 7]
{ 'a'=>1, 'b'=>2, 'c'=>3 }.to_a   #=> [["a", 1], ["b", 2], ["c", 3]]

require 'prime'
Prime.entries 10                  #=> [2, 3, 5, 7]
```

-----
<a name="find"></a>
### find(ifnone = nil) { |obj| block } → obj or nil
### find(ifnone = nil) → an_enumerator

- Passes each entry in enum to block. Returns the first for which block is not false. If no object matches, calls ifnone and returns its result when it is specified, or returns nil otherwise.

- If no block is given, an enumerator is returned instead

```rb
(1..100).detect  => #<Enumerator: 1..100:detect>
(1..100).find    => #<Enumerator: 1..100:find>

(1..10).detect   { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..10).find     { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..100).detect  { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35
(1..100).find    { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35
```


------
<a name="find_all"></a>
### find_all { |obj| block } → array
### find_all → an_enumerator


```rb
(1..10).find_all { |i|  i % 3 == 0 }   #=> [3, 6, 9]

[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]
```

-----
<a name="find_index"></a>
### find_index(value) → int or nil
### find_index { |obj| block } → int or nil
### find_index → an_enumerator

- Compares each entry in enum with value or passes to block. Returns the index for the first for which the evaluated value is non-false. If no object matches, returns nil

- If neither block nor argument is given, an enumerator is returned instead.

```rb
(1..10).find_index  { |i| i % 5 == 0 and i % 7 == 0 }  #=> nil
(1..100).find_index { |i| i % 5 == 0 and i % 7 == 0 }  #=> 34
(1..100).find_index(50)                                #=> 49
```


----
<a name="first"></a>
### first → obj or nil
### first(n) → an_array

```rb
%w[foo bar baz].first     #=> "foo"
%w[foo bar baz].first(2)  #=> ["foo", "bar"]
%w[foo bar baz].first(10) #=> ["foo", "bar", "baz"]
[].first                  #=> nil
[].first(10)              #=> []
```

-------
<a name="flat_map"></a>
### flat_map { |obj| block } → array
### flat_map → an_enumerator
```rb
[1, 2, 3, 4].flat_map { |e| [e, -e] } #=> [1, -1, 2, -2, 3, -3, 4, -4]
[[1, 2], [3, 4]].flat_map { |e| e + [100] } #=> [1, 2, 100, 3, 4, 100]
```


------
<a name="grep"></a>
### grep(pattern) → array
### grep(pattern) { |obj| block } → array

- Returns an array of every element in enum for which Pattern === element. If the optional block is supplied, each matching element is passed to it, and the block’s result is stored in the output array
```rb
(1..100).grep 38..44   #=> [38, 39, 40, 41, 42, 43, 44]
c = IO.constants
c.grep(/SEEK/)         #=> [:SEEK_SET, :SEEK_CUR, :SEEK_END]
res = c.grep(/SEEK/) { |v| IO.const_get(v) }
res                    #=> [0, 1, 2]
```

------
<a name="grep_v"></a>
### grep_v(pattern) → array
### grep_v(pattern) { |obj| block } → array

- Inverted version of #grep. Returns an array of every element in enum for which not Pattern === element.

```rb
(1..10).grep_v 2..5   #=> [1, 6, 7, 8, 9, 10]
res =(1..10).grep_v(2..5) { |v| v * 2 }
res                    #=> [2, 12, 14, 16, 18, 20]
```


-----
<a name="group_by"></a>
### group_by { |obj| block } → a_hash
### group_by → an_enumerator

- Groups the collection by result of the block. Returns a hash where the keys are the evaluated result from the block and the values are arrays of elements in the collection that correspond to the key.

- If no block is given an enumerator is returned.

```rb
(1..6).group_by { |i| i%3 }   #=> {0=>[3, 6], 1=>[1, 4], 2=>[2, 5]}
```


-----
<a name="include?"></a>
### include?(obj) → true or false
- Returns true if any member of enum equals obj. Equality is tested using ==.

```rb
IO.constants.include? :SEEK_SET          #=> true
IO.constants.include? :SEEK_NO_FURTHER   #=> false
IO.constants.member? :SEEK_SET          #=> true
IO.constants.member? :SEEK_NO_FURTHER   #=> false
```


-----
<a name="inject"></a>
### inject(initial, sym) → obj
### inject(sym) → obj
### inject(initial) { |memo, obj| block } → obj
### inject { |memo, obj| block } → obj


```rb
# Sum some numbers
(5..10).reduce(:+)                             #=> 45
# Same using a block and inject
(5..10).inject { |sum, n| sum + n }            #=> 45
# Multiply some numbers
(5..10).reduce(1, :*)                          #=> 151200
# Same using a block
(5..10).inject(1) { |product, n| product * n } #=> 151200
# find the longest word
longest = %w{ cat sheep bear }.inject do |memo, word|
   memo.length > word.length ? memo : word
end
longest                                        #=> "sheep"
```

----
<a name="lazy"></a>
### lazy → lazy_enumerator
- Returns a lazy enumerator, whose methods map/collect, flat_map/collect_concat, select/find_all, reject, grep, #grep_v, zip, take, #take_while, drop, and #drop_while enumerate values only on an as-needed basis. However, if a block is given to zip, values are enumerated immediately.

```rb
def pythagorean_triples
  (1..Float::INFINITY).lazy.flat_map {|z|
    (1..z).flat_map {|x|
      (x..z).select {|y|
        x**2 + y**2 == z**2
      }.map {|y|
        [x, y, z]
      }
    }
  }
end
# show first ten pythagorean triples
p pythagorean_triples.take(10).force # take is lazy, so force is needed
p pythagorean_triples.first(10)      # first is eager
# show pythagorean triples less than 100
p pythagorean_triples.take_while { |*, z| z < 100 }.force
```


------
<a name="map"></a>
### map { |obj| block } → array
### map → an_enumerator

```rb
(1..4).map { |i| i*i }      #=> [1, 4, 9, 16]
(1..4).collect { "cat"  }   #=> ["cat", "cat", "cat", "cat"]
```


-----
<a name="max"></a>
### max → obj
### max { |a, b| block } → obj
### max(n) → array
### max(n) { |a, b| block } → array

- Returns the object in enum with the maximum value. The first form assumes all objects implement Comparable; the second uses the block to return a <=> b.
- If the n argument is given, maximum n elements are returned as an array, sorted in descending order.

```rb
a = %w(albatross dog horse)
a.max                                   #=> "horse"
a.max { |a, b| a.length <=> b.length }  #=> "albatross"
```

- If the n argument is given, maximum n elements are returned as an array, sorted in descending order.


```rb
a = %w[albatross dog horse]
a.max(2)                                  #=> ["horse", "dog"]
a.max(2) {|a, b| a.length <=> b.length }  #=> ["albatross", "horse"]
[5, 1, 3, 4, 2].max(3)                    #=> [5, 4, 3]
```


----
<a name="max_by"></a>
### max_by {|obj| block } → obj
### max_by → an_enumerator
### max_by(n) {|obj| block } → obj
### max_by(n) → an_enumerator

- Returns the object in enum that gives the maximum value from the given block.

- If no block is given, an enumerator is returned instead.

```rb
a = %w(albatross dog horse)
a.max_by { |x| x.length }   #=> "albatross"
```

- If the n argument is given, maximum n elements are returned as an array. These n elements are sorted by the value from the given block, in descending order.

```rb
a = %w[albatross dog horse]
a.max_by(2) {|x| x.length } #=> ["albatross", "horse"]
```

- enum.max_by(n) can be used to implement weighted random sampling. Following example implements and use Enumerable#wsample.

```rb
module Enumerable
  # weighted random sampling.
  #
  # Pavlos S. Efraimidis, Paul G. Spirakis
  # Weighted random sampling with a reservoir
  # Information Processing Letters
  # Volume 97, Issue 5 (16 March 2006)
  def wsample(n)
    self.max_by(n) {|v| rand ** (1.0/yield(v)) }
  end
end
e = (-20..20).to_a*10000
a = e.wsample(20000) {|x|
  Math.exp(-(x/5.0)**2) # normal distribution
}
# a is 20000 samples from e.
p a.length #=> 20000
h = a.group_by {|x| x }
-10.upto(10) {|x| puts "*" * (h[x].length/30.0).to_i if h[x] }
#=> *
#   ***
#   ******
#   ***********
#   ******************
#   *****************************
#   *****************************************
#   ****************************************************
#   ***************************************************************
#   ********************************************************************
#   ***********************************************************************
#   ***********************************************************************
#   **************************************************************
#   ****************************************************
#   ***************************************
#   ***************************
#   ******************
#   ***********
#   *******
#   ***
#   *
```


----
<a name="member?"></a>
### member?(obj) → true or false

- Returns true if any member of enum equals obj. Equality is tested using ==.

```rb
IO.constants.include? :SEEK_SET          #=> true
IO.constants.include? :SEEK_NO_FURTHER   #=> false
IO.constants.member? :SEEK_SET          #=> true
IO.constants.member? :SEEK_NO_FURTHER   #=> false
```

-----
<a name="min"></a>
### min → obj
### min { |a, b| block } → obj
### min(n) → array
### min(n) { |a, b| block } → array

- Returns the object in enum with the minimum value. The first form assumes all objects implement Comparable; the second uses the block to return a <=> b.

```rb
a = %w(albatross dog horse)
a.min                                   #=> "albatross"
a.min { |a, b| a.length <=> b.length }  #=> "dog"
```

- If the n argument is given, minimum n elements are returned as a sorted array.

```rb
a = %w[albatross dog horse]
a.min(2)                                  #=> ["albatross", "dog"]
a.min(2) {|a, b| a.length <=> b.length }  #=> ["dog", "horse"]
[5, 1, 3, 4, 2].min(3)                    #=> [1, 2, 3]
```


----
<a name="min_by"></a>
### min_by {|obj| block } → obj
### min_by → an_enumerator
### min_by(n) {|obj| block } → array
### min_by(n) → an_enumerator

- Returns the object in enum that gives the minimum value from the given block.

- If no block is given, an enumerator is returned instead.

```rb
a = %w(albatross dog horse)
a.min_by { |x| x.length }   #=> "dog"
```


- If the n argument is given, minimum n elements are returned as an array. These n elements are sorted by the value from the given block.

```rb
a = %w[albatross dog horse]
p a.min_by(2) {|x| x.length } #=> ["dog", "horse"]
```

----
<a name="minmax"></a>
### minmax → [min, max]
### minmax { |a, b| block } → [min, max]

- Returns a two element array which contains the minimum and the maximum value in the enumerable. The first form assumes all objects implement Comparable; the second uses the block to return a <=> b.

```rb
a = %w(albatross dog horse)
a.minmax                                  #=> ["albatross", "horse"]
a.minmax { |a, b| a.length <=> b.length } #=> ["dog", "albatross"]
```

----
<a name="minmax_by"></a>
### minmax_by { |obj| block } → [min, max]
### minmax_by → an_enumerator

- Returns a two element array containing the objects in enum that correspond to the minimum and maximum values respectively from the given block.

- If no block is given, an enumerator is returned instead.

```rb
a = %w(albatross dog horse)
a.minmax_by { |x| x.length }   #=> ["dog", "albatross"]
```

----
<a name="none?"></a>
### none? [{ |obj| block }] → true or false

- Passes each element of the collection to the given block. The method returns true if the block never returns true for all elements. If the block is not given, none? will return true only if none of the collection members is true.

```rb
%w{ant bear cat}.none? { |word| word.length == 5 } #=> true
%w{ant bear cat}.none? { |word| word.length >= 4 } #=> false
[].none?                                           #=> true
[nil].none?                                        #=> true
[nil, false].none?                                 #=> true
[nil, false, true].none?                           #=> false
```


----
<a name="one?"></a>
### one? [{ |obj| block }] → true or false

- Passes each element of the collection to the given block. The method returns true if the block returns true exactly once. If the block is not given, one? will return true only if exactly one of the collection members is true.

```rb
%w{ant bear cat}.one? { |word| word.length == 4 }  #=> true
%w{ant bear cat}.one? { |word| word.length > 4 }   #=> false
%w{ant bear cat}.one? { |word| word.length < 4 }   #=> false
[ nil, true, 99 ].one?                             #=> false
[ nil, true, false ].one?                          #=> true
```

----
<a name="partition"></a>
### partition { |obj| block } → [ true_array, false_array ]
### partition → an_enumerator

- Returns two arrays, the first containing the elements of enum for which the block evaluates to true, the second containing the rest.

- If no block is given, an enumerator is returned instead.

```rb
(1..6).partition { |v| v.even? }  #=> [[2, 4, 6], [1, 3, 5]]
```

-----
<a name="reduce"></a>
### reduce(initial, sym) → obj
### reduce(sym) → obj
### reduce(initial) { |memo, obj| block } → obj
### reduce { |memo, obj| block } → obj

- Combines all elements of enum by applying a binary operation, specified by a block or a symbol that names a method or operator.

- The inject and reduce methods are aliases. There is no performance benefit to either.

- If you specify a block, then for each element in enum the block is passed an accumulator value (memo) and the element. If you specify a symbol instead, then each element in the collection will be passed to the named method of memo. In either case, the result becomes the new value for memo. At the end of the iteration, the final value of memo is the return value for the method.

- If you do not explicitly specify an initial value for memo, then the first element of collection is used as the initial value of memo.

```rb
# Sum some numbers
(5..10).reduce(:+)                             #=> 45
# Same using a block and inject
(5..10).inject { |sum, n| sum + n }            #=> 45
# Multiply some numbers
(5..10).reduce(1, :*)                          #=> 151200
# Same using a block
(5..10).inject(1) { |product, n| product * n } #=> 151200
# find the longest word
longest = %w{ cat sheep bear }.inject do |memo, word|
   memo.length > word.length ? memo : word
end
longest                                        #=> "sheep"
```


------
<a name="reject"></a>
### reject { |obj| block } → array
### reject → an_enumerator

- Returns an array for all elements of enum for which the given block returns false.

- If no block is given, an Enumerator is returned instead.

```rb
(1..10).reject { |i|  i % 3 == 0 }   #=> [1, 2, 4, 5, 7, 8, 10]

[1, 2, 3, 4, 5].reject { |num| num.even? } #=> [1, 3, 5]
```

See also [find_all](#find_all).

-----
<a name="reverse_each"></a>

### reverse_each(*args) { |item| block } → enum
### reverse_each(*args) → an_enumerator

- Builds a temporary array and traverses that array in reverse order.

- If no block is given, an enumerator is returned instead.

```rb

  (1..3).reverse_each { |v| p v }

produces:

  3
  2
  1
```


----
<a name="select"></a>
### select { |obj| block } → array click to toggle source
### select → an_enumerator

- Returns an array containing all elements of enum for which the given block returns a true value.

- If no block is given, an Enumerator is returned instead

```rb
(1..10).find_all { |i|  i % 3 == 0 }   #=> [3, 6, 9]

[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]
```
See also [reject](#reject)


----
