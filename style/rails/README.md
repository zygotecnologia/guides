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

# Migrations

## Non-reversible migrations

Use `change` instead of `up` and `down` to create new migrations, but watch out for non-reversible migration commands.
For instance, simply calling `drop_table` inside a `change` will break since ActiveRecord doesn't know what to do in a rollback.
For these special cases, use `up` and `down` to explicitly tell ActiveRecord what to do. All reversible commands can be found
in [CommandRecorder Docs](https://api.rubyonrails.org/classes/ActiveRecord/Migration/CommandRecorder.html)

```ruby
# bad
class AddNameToUsers < ActiveRecord::Migration
  def up
    add_column :users, :name, :string
  end

  def down
    remove_column :users, :name, :string
  end
end

# good - ActiveRecord knows how to rollback
class AddNameToUsers < ActiveRecord::Migration
  def change
    add_column :users, :name, :string
  end
end

# bad - ActiveRecord breaks when rolling back
class DropUsers < ActiveRecord::Migration
  def change
    drop_table :users
  end
end

# good - Now ActiveRecord can rollback
class DropUsers < ActiveRecord::Migration
  def up
    drop_table :users
  end

  def down
    create_table :users do |t|
      t.string :name
    end
  end
end
```

# ActiveSupport Core Extensions

## Safe Navigator over `try!`

Prefer the safe navigator operand (`&.`) over `try!` when nil-checking the left side of an operand.
`try!` is used to protect the right side of an operand, when the left-side is not nil.

```ruby
# bad if obj coulbe be nil
obj.try! :fly

# good
obj&.fly

# good if `obj` is not nil and may or may not have the method `bark`
obj.try! :bark
```

# Routing

## Member collection rules

When you need to add more actions to a RESTful resource, use member and collection routes with block syntax.

```ruby
# bad
get "subscriptions/:id/unsubscribe"
resources :subscriptions

# bad - use block syntax instead
resources :subscriptions do
  get "unsubscribe", on: :member
end

# good
resources :subscriptions do
  member do
    get "unsubscribe"
  end
end

# good
resources :photos do
  collection do
    get "search"
  end
end
```

# Rendering

## Avoid relative path in partial rendering

Using relative path to render a partial in a view leads to a [slower page loading](https://medium.com/wantedly-engineering/a-simple-fix-to-improve-partial-rendering-speed-by-30-in-a-large-rails-application-9696a92f4ae1).
Also, it is very likely to cause a bug when different partials have the same name. So, always use the full path from the `views` folder.

```ruby
# file name: app/views/scope/resource/partial_name
# bad
<%= render "partial_name" %>

# good
<%= render "scope/resource/partial_name" %>
```

# Sidekiq

## Parameter passing

Whenever calling Sidekiq jobs, the parameters sent in the `perform` call must be composed of simple JSON datatypes,
since Sidekiq convert the parameters to JSON in order to store it in Redis, and complex Ruby objects will look like
`#<Quote:0x0000000006e57288>`
From [Sidekiq docs](https://github.com/mperham/sidekiq/wiki/Best-Practices#1-make-your-job-parameters-small-and-simple)

>The arguments you pass to perform_async must be composed of simple JSON datatypes:
> string, integer, float, boolean, null(nil), array and hash.
> This means you must not use ruby symbols as arguments.
> [...] Don't pass symbols, named parameters or complex Ruby objects (like Date or Time!)
> as those will not survive the dump/load round trip correctly.

Remember this includes the usage of `.delay` method when sending emails, since this method schedules a job in Sidekiq.
So the same rule applies when passing parameters to methods after `.delay`/`.delay_until`/`.delay_for`...

When dealing with time, use `.iso8601` to convert it into string and back to Datetime.

```ruby
# bad
class BadReleaseStoreWorker
  include Sidekiq::Worker

  def perform(store, moment)
    return if moment.saturday? || moment.sunday?

    store.update(released_at: moment)
  end
end

BadReleaseStoreWorker.perform_async(Store.last, Time.zone.now)

# good
class GoodReleaseStoreWorker
  include Sidekiq::Worker

  def perform(store_id, moment)
    store = Store.find(store_id)
    moment = moment.to_datetime

    return if moment.saturday? || moment.sunday?

    store.update(released_at: moment)
  end
end

GoodReleaseStoreWorker.perform_async(Store.last.id, Time.zone.now.iso8601)
```