Ruby
====

This Ruby style guide recommends best practices so that real-world Ruby programmers can write code that can be maintained by other real-world Ruby programmers.

- Formatting and spacing
  - File formatting
  - Spaces and Braces
  - Method calls
  - Empty lines

- Naming
  - Boolean Methods Question Mark
  - Boolean Methods Prefix
  - Naming

- Collections
  - `%w`
  - `%i`
  - Percent Literal Braces
  - Empty collections literals
  - Multi-line Hashes
  - Array trailing comma
  - Multi-line Arrays Alignment
  - Symbols as Keys
  - Hashcolon syntax over hashrocket

- Operators
  - No `and` or `or`
  - `!` vs `not`
  - No Space after Bang
  - Double Negation

- Strings
  - String Concatenation
  - Quotes

- Conditionals
  - No Multi-line `if` Modifiers
  - Assignment in condition
  - Indent Conditional Assignment
  - Case
  - `if`/`unless`
  - Ternary Operator
  - No Nested Ternary

- Comments
  - Function comments

- Blocks
  - Single line blocks
  - Single action blocks

- Methods
  - Dangerous Method Bang
  - Define safe using unsafe
  - Single-line Methods
  - Optional parameters
  - `return`
  - Parentheses

- Classes & Modules
  - Consistent Classes
  - Namespace Definition
  - Indent public/private/protected
  - Avoid the usage of class (@@) variables
  - `def self` Class Methods

- Exceptions
  - Control flow
  - Rescuing superclass

- Etc
  - No `for` Loops
  - Ranges or between
  - No `DateTime`
  - `is_a?` and `kind_of?`

---------------------------------------------


# Formatting and spacing
## File formatting
* Use 2 space indentation (no tabs).
* Keep each line of code to a readable length. Unless you have a reason to, keep lines to fewer than 120 characters.
* Never leave trailing whitespace.
* End each file with a newline.

## Spaces and Braces

No spaces after `(`, `[` or before `]`, `)`.

```ruby
# bad
some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good
some(arg).other
[1, 2, 3].each { |e| puts e }
```

For hash literals use spaces around `{` and before `}`.
```ruby
# good
{ one: 1, two: 2 }
```

With interpolated expressions don't use spaces around `{` and before `}`.

```ruby
# bad
"From: #{ user.first_name }, #{ user.last_name }"

# good
"From: #{user.first_name}, #{user.last_name}"
```


## Method calls

Never put a space between a method name and the opening parenthesis.

```ruby
# bad
f (3 + 2) + 1

# good
f(3 + 2) + 1
```

## Empty lines

Insert empty lines between method definitions and between logical paragraphs inside a method.

```ruby
# bad
def do_something
  do_something_else
end
def do_something_else
  2 + 2
end

# good
def do_something
  do_something_else
end

def do_something_else
  2 + 2
end

# also bad
def do_something
  @foo = 'foo'
  @bar = 'bar'
  if @foo == @bar
    puts 'foo is bar'
  else
    puts 'foo is not bar'
  end
  2 + 2
end

# good
def do_something
  @foo = 'foo'
  @bar = 'bar'

  if @foo == @bar
    puts 'foo is bar'
  else
    puts 'foo is not bar'
  end

  2 + 2
end
```

Also, avoid consecutive empty lines.

```ruby
# bad
def do_something
  do_something_else
end


def do_something_else
  2 + 2
end

# good
def do_something
  do_something_else
end

def do_something_else
  2 + 2
end
```

# Naming
## Boolean Methods Question Mark

The names of predicate methods (methods that return a boolean value) should end in a question mark (i.e. `Array#empty?`). Methods that don’t return a boolean, shouldn’t end in a question mark.

## Boolean Methods Prefix

Avoid prefixing predicate methods with the auxiliary verbs such as `is`, `does`, or `can`. These words are redundant and inconsistent with the style of boolean methods in the Ruby core library, such as `empty?` and `include?`.

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

## Casing

* Use **snake_case** for methods and variables.

* Use **CamelCase** for classes and modules. (Keep acronyms like HTTP, RFC, XML uppercase.)

* Use **SCREAMING_SNAKE_CASE** for other constants.

* Name throwaway variables `_`.

  ```ruby
  version = '3.2.1'
  major_version, minor_version, _ = version.split('.')
  ```


# Collections
## `%w`

Prefer `%w` to the literal array syntax when you need an array of words (non-empty strings without spaces and special characters in them). Apply this rule only to arrays with two or more elements.

```ruby
# bad
STATES = ['draft', 'open', 'closed']

# good
STATES = %w[draft open closed]
```

## `%i`

Prefer `%i` to the literal array syntax when you need an array of symbols (and you don’t need to maintain Ruby 1.9 compatibility). Apply this rule only to arrays with two or more elements.

```ruby
# bad
STATES = [:draft, :open, :closed]

# good
STATES = %i[draft open closed]
```

## Percent Literal Braces

Use always `[]` to define percent literals

```ruby
# bad
%q{"Test's king!", John said.}
%w(one two three)
%i(one two three)
%r((\w+)-(\d+))
%r{\w{1,2}\d{2,5}}

# good
%q["Test's king!", John said.]
%w[one two three]
%i[one two three]
%r[(\w+)-(\d+)]
%r[\w{1,2}\d{2,5}]
```

## Empty collections literals

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

## Multi-line Hashes

Use multi-line hashes when it makes the code more readable, and use trailing commas to ensure that parameter changes don't cause extraneous diff lines when the logic has not otherwise changed.

```ruby
hash = {
  protocol: 'https',
  only_path: false,
  controller: :users,
  action: :set_password,
  redirect: @redirect_url,
  secret: @secret,
}
```

## Array trailing comma

Use a trailing comma in an Array that spans more than one line.

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

## Multi-line Arrays Alignment

Align the elements of array literals spanning multiple lines.

```ruby
# bad - single indent
menu_item = %w[Spam Spam Spam Spam Spam Spam Spam Spam
  Baked beans Spam Spam Spam Spam Spam]

# bad
menu_item =
  %w[Spam Spam Spam Spam Spam Spam Spam Spam
     Baked beans Spam Spam Spam Spam Spam]

# good
menu_item = %w[
  Spam Spam Spam Spam Spam Spam Spam Spam
  Baked beans Spam Spam Spam Spam Spam
]

# good
menu_item = %w[Spam Spam Spam Spam Spam Spam Spam Spam
               Baked beans Spam Spam Spam Spam Spam]
```

## Symbols as Keys

Prefer symbols instead of strings as hash keys, except when the use of strings are justified.

```ruby
# bad
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# good
hash = { one: 1, two: 2, three: 3 }

# also good, symbols can't use hyphens
hash = { "twenty-one" => 21, "twenty-two" => 22 }
```

## Hashcolon syntax over hashrocket

Prefer hashcolon syntax for hash definition when every key is a symbol. Use hashrocket syntax if at least one key is not a symbol.

```ruby
# bad
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# bad
hash = { twenty: 20, "twenty-one" => 21 }

# good
hash = { one: 1, two: 2, three: 3 }

# also good, symbols can't use hyphens
hash = { "twenty" => 20, "twenty-one" => 21 }
```

# Operators
## No `and` or `or`

The `and` and `or` keywords are banned. They aren't alias to `&&` and `||` operators, so they shouldn't be used like so. For boolean expressions, always use `&&` and `||`. For flow control, use `if` and `unless`; `&&` and `||` are also acceptable but less clear.

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

## `!` vs `not`

Use `!` instead of `not`.

```ruby
# bad - parentheses are required because of op precedence
x = (not something)

# good
x = !something
```

## No Space after Bang

No space after `!`.

```ruby
# bad
! something

# good
!something
```

## Double Negation

Avoid the use of `!!`.

`!!` converts a value to boolean, but you don’t need this explicit conversion in the condition of a control expression; using it only obscures your intention. If you want to do a `nil` check, use `nil?` instead.

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


# Strings
## String Concatenation

Avoid using `String#+` when you need to construct large data chunks. Instead, use `String#<<`. Concatenation mutates the string instance in-place and is always faster than `String#+`, which creates a bunch of new string objects.

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

## Quotes

Use double-quoted strings, and prefer string interpolation over string concatenation.

```ruby
# bad
my_string = 'example'

# good
my_string = "example"

# bad
my_string = "Name: " + name

# good
my_string = "Name: #{name}"
```

# Conditionals
## No Multi-line `if` Modifiers

Avoid modifier `if`/`unless` usage at the end of a non-trivial multi-line block.

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

## Assignment in condition

Don't use the return value of `=` in conditionals.

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

## Indent Conditional Assignment

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

## Case indentation

Indent `when` as deep as `case`.

```ruby
# bad
case days
  when 0
    "Zero days"
  when 1
    "One day"
  when 2
    "Two days"

# good
case days
when 0
  "Zero days"
when 1
  "One day"
when 2
  "Two days"
```

## `if`/`unless`

Never use `then` for multiline statements.
Never use `unless` with `else`. Rewrite these with the positive case first.
Don't use parentheses around the condition.

```ruby
# bad
unless(condition) then
  ...
else
  ...
end

# good
if condition
  ...
else
  ...
end
```

## Ternary Operator

Ternary operator should be simple and easy to read, so use one expression per branch, and none boolean algebra.

```ruby
# bad
result = (some_condition || another_condition) && !not_this_one ? something : something_else

# bad
some_condition ? (puts("condition is true"); call_if_true(condition)) : (puts("condition is false"))

# good
result = some_condition ? something : something_else
```

### No Nested Ternary

_(to keep the simplicity spoken above)_ Ternary operators must not be nested. Prefer `if/else` constructs in these cases.

```ruby
# bad
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# good
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```

# Comments
## Function comments

Use explanatory comments only before a method definition. This means that no comment should be written between logic to avoid confusion and lost of train of thought.
Whenever you feel the need to add comment inside a method, that probably means this piece of code could (and should) be extracted to a new method.

```ruby
# bad
def big_method
  foo = bar if baz?
  bar = foo if baz?

  # this iterator does xyz because of abc after jkl is qrs
  foo.each do |f|
    f.var = bar.var[0..2]
    f.touch(:new_var_at)
  end

  bar = baz * foo
end

# good
def big_method
  foo = bar if baz?
  bar = foo if baz?

  complex_thing(foo, bar)

  bar = baz * foo
end

# this iterator does xyz because of abc after jkl is qrs
def complex_thing(foo, bar)
  foo.each do |f|
    f.var = bar.var[0..2]
    f.touch(:new_var_at)
  end
end
```

# Blocks
## Single line blocks

Prefer `{ ... }` over `do ... end` for single-line blocks. Avoid using `{ ... }` for multi-line blocks (multiline chaining is always ugly). Always use `do ... end` for "control flow" and "method definitions" (e.g. in Rakefiles and certain DSLs). Avoid `do ... end` when chaining.

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

## Single action blocks

When a method block takes only one argument, and the body consists solely of reading an attribute or calling one method with no arguments, use the `&:` shorthand.

```ruby
# bad
bluths.map { |bluth| bluth.occupation }
bluths.select { |bluth| bluth.blue_self? }

# good
bluths.map(&:occupation)
bluths.select(&:blue_self?)
```

# Methods
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
# bad
class MyService
  def call!(id)
    MyModel.find(id)
  end

  def call(id)
    MyModel.find_by(id: id)
  end
end

# good
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

## Single-line Methods

Avoid single-line methods that have a body.

```ruby
# bad
def too_much; something; end

# good
def some_method
  something
end
```

Avoid defining methods in multiple lines if they have no actual body.

```ruby
# bad
def index
end

# good
def index; end
```

## Optional parameters

Use the options-hash as optional parameters instead of using default parameters for better argument clarification.
Also, omit the hash declaration and brackets for simplicity.

```ruby
# bad
def remove_member(user, skip_membership_check = false)
  # ...
end

# elsewhere, out of the method definition context: what does `true` means here?
remove_member(user, true)


# good
def remove_member(user, skip_membership_check: false)
  # ...
end

# elsewhere, out of the method definition context: ok, now i know what it means
remove_member(user, skip_membership_check: true)
```

## `return`

Avoid `return` where not required.

```ruby
# bad
def my_sum(a, b)
  return a + b
end

# good
def my_sum(a, b)
  a + b
end
```

## Parentheses

Use parentheses when there are arguments. Omit the parentheses when the method doesn't accept any arguments.

```ruby
# bad
def my_function()
  ...
end

# good
def my_function
  ...
end

# bad
def my_function a, b
  ...
end

# good
def my_function(a, b)
  ...
end
```

# Classes & Modules
## Consistent Classes

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

## Namespace Definition

Define (and reopen) namespaced classes and modules using explicit nesting.

```ruby
# bad
class Utilities::Store
  # ...
end

# good
module Utilities
  class WaitingList
    # ...
  end
end
```

## Indent public/private/protected

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

## Avoid the usage of class (@@) variables

Avoid the usage of class (`@@`) variables due to their "nasty" behavior in inheritance.

```ruby
class Parent
  @@class_var = 'parent'

  def self.print_class_var
    puts @@class_var
  end
end

class Child < Parent
  @@class_var = 'child'
end

Parent.print_class_var # => will print "child"
```

## `def self` Class Methods

Use `self.method` to define class methods. This makes the code easier to refactor since the class name is not repeated.

```ruby
class TestClass
  # bad
  def TestClass.some_method
    # body omitted
  end

  # good
  def self.some_other_method
    # body omitted
  end
end
```

# Exceptions
## Control flow

Don't use exceptions for flow of control, when easily avoidable.

```ruby
# bad
begin
  n / d
rescue ZeroDivisionError
  puts "Cannot divide by 0!"
end

# good
if d.zero?
  puts "Cannot divide by 0!"
else
  n / d
end
```

## Rescuing superclass

Do not rescue `StandardError` or its superclass `Exception`

```ruby
# bad
begin
  2 / 0
rescue Exception
  puts "Can't divide by zero"
end

# also bad
begin
  2 / 0
rescue StandardError
  puts "Can't divide by zero"
end

# good
begin
  2 / 0
rescue ZeroDivisionError
  puts "Can't divide by zero"
end
```

# Etc
## No `for` Loops

Do not use `for`, unless you know exactly why. Most of the time iterators should be used instead. `for` is implemented in terms of `each` (so you’re adding a level of indirection), but with a twist - `for` doesn’t introduce a new scope (unlike `each`) and variables defined in its block will be visible outside it.

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

## Ranges or between

Use ranges or `Comparable#between?` instead of complex comparison logic when possible.

```ruby
# bad
do_something if x >= 1000 && x <= 2000

# good
do_something if (1000..2000).include?(x)

# good
do_something if x.between?(1000, 2000)
```

## No `DateTime`

Don’t use `DateTime` unless you need to account for historical calendar reform - and if you do,
explicitly specify the start argument to clearly state your intentions.

Use `Time.zone`.

```ruby
# bad
DateTime.now

# bad - missing timezone
Time.now

# good
Time.zone.now
```

## `is_a?` and `kind_of?`

Don't use `===` operator, instead use `is_a?` or `kind_of?`.

```ruby
# bad
if String === my_variable
  "is a string"
end

# good
if my_variable.is_a?(String)
  "is a string"
end
```
