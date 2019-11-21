Ruby
====

This Ruby style guide recommends best practices so that real-world Ruby programmers can write code that can be maintained by other real-world Ruby programmers.

## Bang Methods

They are questions, and do not modify the object they are called on.

For example:

```ruby
name = "Ruby Monstas"
puts name.downcase
puts name
```

This will output:

```text
ruby monstas
Ruby Monstas
```

As you can see the method downcase has returned a new String, which is the lowercase version of the String that the method is being called on. When we output the original String on the next line, we can then see that it’s still the same: The method downcase does not modify the String.

However, there also are variants of some of these methods, which end in an exclamation mark !. These methods are called “bang methods”, and they usually modify the object that they’re being called on.

> Bang methods end with an exlamation mark, and often modify the object they are called on.

For example, next to the method downcase Strings also have a method downcase!.

Let’s try that:

```ruby
name = "Ruby Monstas"
puts name.downcase!
puts name
```

This will output:

```text
ruby monstas
ruby monstas
```

As you can see calling the method downcase! on the second line has modified the String itself (the object that name refers to), and also returned the new downcased version.

> Use bang methods with caution!

## Dangerous Method Bang

The names of potentially _dangerous_ methods (i.e. methods that modify `self` or the arguments, `exit!` (doesn't run the finalizers like `exit` does), etc) should end with an exclamation mark if there exists a safe version of that _dangerous_ method.

```ruby
# bad - there is no matching 'safe' method
class Person
  def update!
  end
end

# good
class Person
  def update
  end
end

# good
class Person
  def update!
  end

  def update
  end
end
```

## Define safe using unsafe

Define the non-bang (safe) method in terms of the bang (dangerous) one if possible.

```ruby
class MyService
  def call!(id)
    MyModel.find(id)
  end

  def call(id)
    call!(id)
  rescue ActiveRecord::RecordNotFound
    nil
  end
end
```

## Spaces and Braces

No spaces after (, [ or before ], ). Use spaces around { and before }.

```ruby
# bad
some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good
some(arg).other
[1, 2, 3].each { |e| puts e }
{ and } deserve a bit of clarification, since they are used for block and hash literals, as well as string interpolation.
```

For hash literals two styles are considered acceptable. The first variant is slightly more readable (and arguably more popular in the Ruby community in general). The second variant has the advantage of adding visual difference between block and hash literals. Whichever one you pick - apply it consistently.

```ruby
# good - space after { and before }
{ one: 1, two: 2 }

# good - no space after { and before }
{one: 1, two: 2}
```

With interpolated expressions, there should be no padded-spacing inside the braces.

```ruby
# bad
"From: #{ user.first_name }, #{ user.last_name }"

# good
"From: #{user.first_name}, #{user.last_name}"
```

## No and or or

The and and or keywords are banned. The minimal added readability is just not worth the high probability of introducing subtle bugs. For boolean expressions, always use && and || instead. For flow control, use if and unless; && and || are also acceptable but less clear.

```ruby
# bad
# boolean expression
ok = got_needed_arguments and arguments_are_valid

# control flow
document.save or raise("Failed to save document!")

# good
# boolean expression
ok = got_needed_arguments && arguments_are_valid

# control flow
raise("Failed to save document!") unless document.save

# ok
# control flow
document.save || raise("Failed to save document!")
```

## No Multi-line if Modifiers

Avoid modifier if/unless usage at the end of a non-trivial multi-line block.

```ruby
# bad
10.times do
  # multi-line body omitted
end if some_condition

# good
if some_condition
  10.times do
    # multi-line body omitted
  end
end
```

## %w

Prefer %w to the literal array syntax when you need an array of words (non-empty strings without spaces and special characters in them). Apply this rule only to arrays with two or more elements.

```ruby
# bad
STATES = ['draft', 'open', 'closed']

# good
STATES = %w[draft open closed]
```

## %i

Prefer %i to the literal array syntax when you need an array of symbols (and you don’t need to maintain Ruby 1.9 compatibility). Apply this rule only to arrays with two or more elements.

```ruby
# bad
STATES = [:draft, :open, :closed]

# good
STATES = %i[draft open closed]
```

## Symbols as Keys

Prefer symbols instead of strings as hash keys.

```ruby
# bad
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# good
hash = { one: 1, two: 2, three: 3 }
```

## Boolean Methods Question Mark

The names of predicate methods (methods that return a boolean value) should end in a question mark (i.e. Array#empty?). Methods that don’t return a boolean, shouldn’t end in a question mark.

## Boolean Methods Prefix

Avoid prefixing predicate methods with the auxiliary verbs such as is, does, or can. These words are redundant and inconsistent with the style of boolean methods in the Ruby core library, such as empty? and include?.

```ruby
# bad
class Person
  def is_tall?
    true
  end

  def can_play_basketball?
    false
  end

  def does_like_candy?
    true
  end
end

# good
class Person
  def tall?
    true
  end

  def basketball_player?
    false
  end

  def likes_candy?
    true
  end
end
```

## No for Loops

Do not use for, unless you know exactly why. Most of the time iterators should be used instead. for is implemented in terms of each (so you’re adding a level of indirection), but with a twist - for doesn’t introduce a new scope (unlike each) and variables defined in its block will be visible outside it.

```ruby
arr = [1, 2, 3]

# bad
for elem in arr do
  puts elem
end

# note that elem is accessible outside of the for loop
elem # => 3

# good
arr.each { |elem| puts elem }

# elem is not accessible outside each's block
elem # => NameError: undefined local variable or method `elem'
```

## ! vs not

Use ! instead of not.

```ruby
# bad - parentheses are required because of op precedence
x = (not something)

# good
x = !something
```

## No Space after Bang

No space after !.

```ruby
# bad
! something

# good
!something
```

## Method calls

Never put a space between a method name and the opening parenthesis.

```ruby
# bad
f (3 + 2) + 1

# good
f(3 + 2) + 1
```

## Syntax


### Single line blocks

Prefer {...} over do...end for single-line blocks. Avoid using {...} for multi-line blocks (multiline chaining is always ugly). Always use do...end for "control flow" and "method definitions" (e.g. in Rakefiles and certain DSLs). Avoid do...end when chaining.[link]

```ruby
names = ["Bozhidar", "Steve", "Sarah"]

# good
names.each { |name| puts name }

# bad
names.each do |name| puts name end

# good
names.each do |name|
  puts name
  puts 'yay!'
end

# bad
names.each { |name|
  puts name
  puts 'yay!'
}

# good
names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

# bad
names.select do |name|
  name.start_with?("S")
end.map { |name| name.upcase }
```

### Assignment in condition

Don't use the return value of = in conditionals.

```ruby
# bad - shows intended use of assignment
if (v = array.grep(/foo/))
  ...
end

# bad
if v = array.grep(/foo/)
  ...
end

# good
v = array.grep(/foo/)
if v
  ...
end
```

### Single action blocks

When a method block takes only one argument, and the body consists solely of reading an attribute or calling one method with no arguments, use the &: shorthand. [link]

```ruby
# bad
bluths.map { |bluth| bluth.occupation }
bluths.select { |bluth| bluth.blue_self? }

# good
bluths.map(&:occupation)
bluths.select(&:blue_self?)
```

## Naming

* Use snake_case for methods and variables.

* Use CamelCase for classes and modules. (Keep acronyms like HTTP, RFC, XML uppercase.)

* Use SCREAMING_SNAKE_CASE for other constants.

* The names of predicate methods (methods that return a boolean value) should end in a question mark. (i.e. Array#empty?).

* The names of potentially "dangerous" methods (i.e. methods that modify self or the arguments, exit!, etc.) should end with an exclamation mark. Bang methods should only exist if a non-bang method exists. (More on this.)

* Name throwaway variables `_`.

  ```ruby
  version = '3.2.1'
  major_version, minor_version, _ = version.split('.')
  ```

## Collections

### Empty collections literals

Prefer literal array and hash creation notation unless you need to pass parameters to their constructors.

```ruby
# bad
arr = Array.new
hash = Hash.new

# good
arr = []
hash = {}

# good because constructor requires parameters
x = Hash.new { |h, k| h[k] = {} }
```

### Multi-line Hashes

Use multi-line hashes when it makes the code more readable, and use trailing commas to ensure that parameter changes don't cause extraneous diff lines when the logic has not otherwise changed.

```ruby
hash = {
  :protocol => 'https',
  :only_path => false,
  :controller => :users,
  :action => :set_password,
  :redirect => @redirect_url,
  :secret => @secret,
}
```

### Array trailing comma

Use a trailing comma in an Array that spans more than 1 line[link]

```ruby
# good
array = [1, 2, 3]

# good
array = [
  "car",
  "bear",
  "plane",
  "zoo",
]
```

## No Single-line Methods

Avoid single-line methods. Although they are somewhat popular in the wild, there are a few peculiarities about their definition syntax that make their use undesirable. At any rate - there should be no more than one expression in a single-line method.

```ruby
# bad
def too_much; something; something_else; end

# okish - notice that the first ; is required
def no_braces_method; body end

# okish - notice that the second ; is optional
def no_braces_method; body; end

# okish - valid syntax, but no ; makes it kind of hard to read
def some_method() body end

# good
def some_method
  body
end
```

## Percent Literal Braces

Use the braces that are the most appropriate for the various kinds of percent literals.

* () for string literals (%q, %Q).

* [] for array literals (%w, %i, %W, %I) as it is aligned with the standard array literals.

* {} for regexp literals (%r) since parentheses often appear inside regular expressions. That’s why a less common character with { is usually the best delimiter for %r literals.

* () for all other literals (e.g. %s, %x)

```ruby
# bad
%q{"Test's king!", John said.}

# good
%q("Test's king!", John said.)

# bad
%w(one two three)
%i(one two three)

# good
%w[one two three]
%i[one two three]

# bad
%r((\w+)-(\d+))
%r{\w{1,2}\d{2,5}}

# good
%r{(\w+)-(\d+)}
%r|\w{1,2}\d{2,5}|
```

## Ranges or between

Use ranges or Comparable#between? instead of complex comparison logic when possible.

```ruby
# bad
do_something if x >= 1000 && x <= 2000

# good
do_something if (1000..2000).include?(x)

# good
do_something if x.between?(1000, 2000)
```

## No DateTime

Don’t use DateTime unless you need to account for historical calendar reform - and if you do, explicitly specify the start argument to clearly state your intentions.

```ruby
# bad - uses DateTime for current time
DateTime.now

# good - uses Time for current time
Time.now

# bad - uses DateTime for modern date
DateTime.iso8601('2016-06-29')

# good - uses Date for modern date
Date.iso8601('2016-06-29')

# good - uses DateTime with start argument for historical date
DateTime.iso8601('1751-04-23', Date::ENGLAND)
```

## String Concatenation

Avoid using String#+ when you need to construct large data chunks. Instead, use String#<<. Concatenation mutates the string instance in-place and is always faster than String#+, which creates a bunch of new string objects.

```ruby
# bad
html = ''
html += '<h1>Page title</h1>'

paragraphs.each do |paragraph|
  html += "<p>#{paragraph}</p>"
end

# good and also fast
html = ''
html << '<h1>Page title</h1>'

paragraphs.each do |paragraph|
  html << "<p>#{paragraph}</p>"
end
```

## Classes & Modules

### Consistent Classes

Use a consistent structure in your class definitions.

```ruby
class Person
  # extend and include go first
  extend SomeModule
  include AnotherModule

  # inner classes
  CustomError = Class.new(StandardError)

  # constants are next
  SOME_CONSTANT = 20

  # afterwards we have attribute macros
  attr_reader :name

  # followed by other macros (if any)
  validates :name

  # public class methods are next in line
  def self.some_method
  end

  # initialization goes between class methods and other instance methods
  def initialize
  end

  # followed by other public instance methods
  def some_method
  end

  # protected and private methods are grouped near the end
  protected

  def some_protected_method
  end

  private

  def some_private_method
  end
end
```

### Namespace Definition

Define (and reopen) namespaced classes and modules using explicit nesting. Using the scope resolution operator can lead to surprising constant lookups due to Ruby’s lexical scoping, which depends on the module nesting at the point of definition.

```ruby
module Utilities
  class Queue
  end
end

# bad
class Utilities::Store
  Module.nesting # => [Utilities::Store]

  def initialize
    # Refers to the top level ::Queue class because Utilities isn't in the
    # current nesting chain.
    @queue = Queue.new
  end
end

# good
module Utilities
  class WaitingList
    Module.nesting # => [Utilities::WaitingList, Utilities]

    def initialize
      @queue = Queue.new # Refers to Utilities::Queue
    end
  end
end
```

### Indent public/private/protected

Indent the public, protected, and private methods as much as the method definitions they apply to. Leave one blank line above the visibility modifier and one blank line below in order to emphasize that it applies to all methods below it.

```ruby
# good
class SomeClass
  def public_method
    # some code
  end

  private

  def private_method
    # some code
  end

  def another_private_method
    # some code
  end
end
```

## Source Code Layout

> Nearly everybody is convinced that every style but their own is ugly and unreadable. Leave out the "but their own" and they’re probably right…​

— Jerry Coffin (on indentation)

### Indent Conditional Assignment

When assigning the result of a conditional expression to a variable, preserve the usual alignment of its branches.

```ruby
# bad - pretty convoluted
kind = case year
when 1850..1889 then 'Blues'
when 1890..1909 then 'Ragtime'
when 1910..1929 then 'New Orleans Jazz'
when 1930..1939 then 'Swing'
when 1940..1950 then 'Bebop'
else 'Jazz'
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# good - it's apparent what's going on
kind = case year
       when 1850..1889 then 'Blues'
       when 1890..1909 then 'Ragtime'
       when 1910..1929 then 'New Orleans Jazz'
       when 1930..1939 then 'Swing'
       when 1940..1950 then 'Bebop'
       else 'Jazz'
       end

result = if some_cond
           calc_something
         else
           calc_something_else
         end

# good (and a bit more width efficient)
kind =
  case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  when 1910..1929 then 'New Orleans Jazz'
  when 1930..1939 then 'Swing'
  when 1940..1950 then 'Bebop'
  else 'Jazz'
  end

result =
  if some_cond
    calc_something
  else
    calc_something_else
  end
```

## Flow of Control

### Double Negation

Avoid the use of !!.

!! converts a value to boolean, but you don’t need this explicit conversion in the condition of a control expression; using it only obscures your intention. If you want to do a nil check, use nil? instead.

```ruby
# bad
x = 'test'
# obscure nil check
if !!x
  # body omitted
end

# good
x = 'test'
if x
  # body omitted
end
```
