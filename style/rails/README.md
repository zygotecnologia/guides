Rails
====
This Rails style guide recommends best practices so that real-world Rails programmers can write code that can be maintained by other real-world Rails programmers.

# Models

## ActiveRecord

### Enums

Prefer using the hash syntax for `enum`. Array makes the database values implicit and any insertion/removal/rearrangement of values in the middle will most probably lead to broken code.
It also makes it easier to identify the key-value pair.

```ruby
class Transaction < ActiveRecord::Base
  # bad - implicit values - ordering matters
  enum type: %i[credit debit]

  # good - explicit values - ordering does not matter
  enum type: {
    credit: 0,
    debit: 1
  }
end
```

### `has_many :through`

Prefer `has_many :through` to `has_and_belongs_to_many` when dealing with many-to-many associations.
Using `has_many :through` allows additional attributes and validations on the join model.

```ruby
# bad
class User < ActiveRecord::Base
  has_and_belongs_to_many :groups
end

class Group < ActiveRecord::Base
  has_and_belongs_to_many :users
end

# good
class User < ActiveRecord::Base
  has_many :memberships
  has_many :groups, through: :memberships
end

class Membership < ActiveRecord::Base
  belongs_to :user
  belongs_to :group
end

class Group < ActiveRecord::Base
  has_many :memberships
  has_many :users, through: :memberships
end
```

### Validations with `validate`

Always use validations with `validate :attribute, something` instead of `validates_something_of :attribute`

```ruby
# bad
validates_presence_of :email
validates_length_of :email, maximum: 100

# good
validates :email, presence: true, length: { maximum: 100 }
```

### Never use `default_scope`

Never, under any circunstance, define an `default_scope` inside an model, as it makes debugging much harder.
But if you stumble upon a model that already has an `default_scope` defined, do not remove it, as it will much probably break a lot of code.

```ruby
# bad - if it's you the one who's adding it
class Order < ActiveRecord::Base
  default_scope { where.not(status: :cancelled) }
end

# good
class Order < ActiveRecord::Base
  scope :not_cancelled { where.not(status: :cancelled) }
end
```

## ActiveRecord Queries

### Avoid interpolation

Avoid string interpolation in ActiveRecord Queries, as it will make your code susceptible to SQL injection attacks.

```ruby
# bad
User.where("name LIKE %#{params[:partial_name]}%")

# good
User.where("name LIKE ?", "%#{params[:partial_name]}%")
```

### `size` over `count`

When querying Active Record collections, prefer `size` or `length` over `count`.
Using `length` will load the collection in memory and then count the elements in the array.
As for `size`, it will decide to execute `length` or `count`, depending on whether the collection is already loaded or not.
`count` will ALWAYS execute an SQL query when called in an ActiveRecord object.

```ruby
# bad
User.count

# good
User.all.size

# good - if you really need to load all users into memory
User.all.length
```
