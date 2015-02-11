##Descriptions of Iterators

###Instructions
Below you will find a list of methods. In the space provided below each, please provide a brief description of what this method does based upon your review of the Docs. 

#### Enumerable:
is Ruby's way of saying that we can get elements out of a collection, one at a time.

#### Enumerator
objectification of enumeration. The point of these methods returning these enumerators is to allow us to chain operations indefinitely and make more heavy-duty collections.

###Array methods:
May be helpful to look in [Enumerable](http://ruby-doc.org/core-2.2.0/Enumerable.html) as well...

####select:
returns an array containing all elements after it passes through a condition of enum for which the given block returns a true value

EX: [1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]

	
####reject:
Returns an array for all elements after it passes through a condition for which the given block returns false

EX:  [1, 2, 3, 4, 5].reject { |num| num.even? } #=> [1, 3, 5]

####map:
Returns a NEW array with the results of running block once for every element in enum

EX:  (1..4).map { |i| i*i }      #=> [1, 4, 9, 16]

####detect:
Passes each entry to enum to block.  Returns the FIRST element which the block is NOT FALSE after the condition.  Only returns one/ the first value. If there's no true value then it will result in an nil.

EX: (1..20).detect   { |i| i % 5 == 0}   #=> 5

####inject:
it's the same as reduce:
Cobines all elements by applying a binary operation, specified by a block or a symbol.

EX:  longest = %w{ cat sheep bear }.inject do |memo, word|
   memo.length > word.length ? memo : word
end
longest  

EX: (5..10).inject { |sum, n| sum + n }            #=> 45            


####partition:
Returns two arrays, first cotaining the elements of enum for which the block evalates to true and the second containing the rest.

EX: 
(1..6).partition { |v| v.even? }  #=> [[2, 4, 6], [1, 3, 5]]

####sort:
Returns an array containing the items enum sorted. If it is an array of strings then it will return alphabetical order. If it's numbers then it will be from least to greatest.  If you have a condition

EX: animals = ["dog", "cat", "duck", "hat"]
animals.sort
=> ["cat", "dog", "duck", "hat"]

EX:(with a comparative operator) (1..10).sort { |a, b| b <=> a }  #=> [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

####one:
If EXACTLY one of the elements matches the condition is true will pass true, else it will return false

EX:
%w{ant bear cat}.one? { |word| word.length == 4 }  #=> true

EX:

[ nil, true, 99 ].one?                             #=> false
[ nil, true, false ].one?                          #=> true

Numbers and words are considered truthy values

####none:
Returns true if none of the elements in the collection passes the condition as true

EX:
%w{ant bear cat}.none? { |word| word.length == 5 } #=> true
%w{ant bear cat}.none? { |word| word.length >= 4 } #=> false

EX: FOR FALSEY STATEMENTS
[].none?                                           #=> true
[nil].none?                                        #=> true
[nil, false].none?                                 #=> true

####all:
If all elements pass the condtion as true it will return true.  If one of them is false then it will return false

EX:

%w[ant bear cat].all? { |word| word.length >= 3 } #=> true
%w[ant bear cat].all? { |word| word.length >= 4 } #=> false
[nil, true, 99].all?                              #=> false

####empty?:
- It is Ruby method
- can be used on strings, arrays and hashes and returns true if:


String length == 0
Array length == 0
Hash length == 0
- Running .empty? on something that is nil will throw a NoMethodError
EX:

"".empty = true
" ".empty? = false


####eql?:
checks if two values are equal and of the same type

EX:

irb(main):013:0> val = 17
=> 17
irb(main):014:0> val == 17.0
=> true
irb(main):015:0> val.eql?(17.0)
=> false
irb(main):016:0> val.eql?(17)
=> true
irb(main):017:0> val.equal?(17)
=> true 

####include?:
checking if the value is in the enum

EX: a = [ "a", "b", "c" ]
a.include?("b")   #=> true
a.include?("z")   #=> false

####nil?:
- It is Ruby method
- It can be used on any object and is true if the object is nil.
- "Only the object nil responds true to nil?" - RailsAPI


EX:
nil.nil? = true
anthing_else.nil? = false
a = nil
a.nil? = true
“”.nil = false

###Hash methods:

####key?:
Returns true if the given key is present in the hash

EX:
h = { "a" => 100, "b" => 200 }
h.has_key?("a")   #=> true
h.has_key?("z")   #=> false


####keys:
Returns a new array populated with the keys from the hash

h = { "a" => 100, "b" => 200, "c" => 300, "d" => 400 }
h.keys   #=> ["a", "b", "c", "d"]

####delete:
deletes a key-value pair and returns the value from the hash


EX:
h = { "a" => 100, "b" => 200, "c" => 300, "d" => 400 }
=> {"a"=>100, "b"=>200, "c"=>300, "d"=>400}
 h.delete("b")
=> 200
 h
=> {"a"=>100, "c"=>300, "d"=>400}

####delete_if:
Deletes every key-value pair from hash for which block evaluates to true.  It has a condition.

EX:
h = { "a" => 100, "b" => 200, "c" => 300 }
h.delete_if {|key, value| key >= "b" }   #=> {"a"=>100}

