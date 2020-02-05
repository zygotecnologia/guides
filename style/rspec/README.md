RSpec
=====

Behaviour Driven Development for Ruby. Making TDD Productive and Fun.

### `not_to` vs `to_not`
Write `not_to`. `to_not` leads to a [split infinitive](https://en.wikipedia.org/wiki/Split_infinitive), a not-so-pleasant grammatical construct.

### `#` before instance method describe
Add a `#` before the method name when describing instance methods.

```ruby
describe '#my_method' do
  # ...
end
```

### `#` before class method describe
Add a `.` before the method name when describing class methods.

```ruby
describe '.class_method' do
  # ...
end
```

### Avoid `should` on spec description
Avoid starting your spec description with `should`. It clutters the description without adding much value.

```ruby
# bad
it 'should return something' do
end

# good
it 'returns something' do
  # spec here
end
```

### Keep your description short
Keep your description short. Long descriptions can be avoided making better usage of `context`s and `describe`s.

```ruby
# bad
it 'has 422 status code if an unexpected params will be added' do

# good
context 'when not valid' do
  it { is_expected.to respond_with 422 }
end
```

### Built-in matchers
Use built-in matchers. This includes usage of shoulda-matchers.

```ruby
# bad
it 'includes a title' do
  expect(article.title.include?('a lengthy title')).to be true
end

# good
it 'includes a title' do
  expect(article.title).to include 'a lengthy title'
end
```

### Predicate Matchers
Use RSpec’s predicate matcher methods when possible.

```ruby
# bad
it 'is published' do
  expect(subject.published?).to be true
end

# good
it 'is published' do
  expect(subject).to be_published
end
```

### Context Descriptions

Context descriptions should describe the conditions shared by all the examples within. Full example names (formed by concatenation of all nested block descriptions) should form a readable sentence.

A typical description will be an adjunct phrase starting with 'when', 'with', 'without', or similar words.

```ruby
# bad - 'Summary user is logged in no display name shows a placeholder'
describe 'Summary' do
 context 'user logged in' do
   context 'no display name' do
     it 'shows a placeholder' do
     end
   end
 end
end

# good - 'Summary when the user is logged in when the display name is blank shows a placeholder'
describe 'Summary' do
 context 'when the user is logged in' do
   context 'when the display name is blank' do
     it 'shows a placeholder' do
     end
   end
 end
end
```

### Context Cases

`context` blocks should pretty much always have an opposite negative case.
It is a code smell if there is a single context (without a matching negative case), and this code needs refactoring, or may have no purpose.

```ruby
# bad - needs refactoring
describe '#attributes' do
  context 'the returned hash' do
    it 'includes the display name' do
      # ...
    end

    it 'includes the creation time' do
      # ...
    end
  end
end

# bad - the negative case needs to be tested, but isn't
describe '#attributes' do
  context 'when display name is present' do
    before do
      subject.display_name = 'something'
    end

    it 'includes the display name' do
      # ...
    end
  end
end

# good
describe '#attributes' do
  subject { FactoryBot.create(:article) }

  specify do
    expect(subject.attributes).to include subject.display_name
    expect(subject.attributes).to include subject.created_at
  end
end

describe '#attributes' do
  context 'when display name is present' do
    before do
      subject.display_name = 'something'
    end

    it 'includes the display name' do
      # ...
    end
  end

  context 'when display name is not present' do
    before do
      subject.display_name = nil
    end

    it 'does not include the display name' do
      # ...
    end
  end
end
```

### Stub HTTP Requests

Stub HTTP requests when the code is making them.
Avoid hitting real external services.

Use https://github.com/vcr/vcr[VCR].

```ruby
# good
context 'with unauthorized access' do
  let(:uri) { 'http://api.lelylan.com/types' }

  before { stub_request(:get, uri).to_return(status: 401, body: fixture('401.json')) }

  it 'returns access denied' do
    page.driver.get uri
    expect(page).to have_content 'Access denied'
  end
end
```

### Dealing with Time

Always use https://github.com/travisjeffery/timecop[Timecop] instead of stubbing anything on Time or Date.

```ruby
# bad
it 'offsets the time 2 days into the future' do
  current_time = Time.now
  allow(Time).to receive(:now).and_return(current_time)
  expect(subject.get_offset_time).to eq(current_time + 2.days)
end

# good
it 'offsets the time 2 days into the future' do
  Timecop.freeze(Time.now) do
    expect(subject.get_offset_time).to eq 2.days.from_now
  end
end
```

### Factories

Use https://github.com/thoughtbot/factory_bot[Factory Bot] to create test data in integration tests.
You should very rarely have to use `ModelName.create` within an integration spec.
Do *not* use fixtures as they are not nearly as maintainable as factories.

```ruby
# bad
subject(:article) do
  Article.create(
    title: 'Piccolina',
    author: 'John Archer',
    published_at: '17 August 2172',
    approved: true
  )
end

# good
subject(:article) { FactoryBot.create(:article) }
```

### `before`/`after` that are not for each it

Avoid using `before`/`after` with `:context`/`:all` scope.
Beware of the state leakage between the examples.

### Redundant `before(:each)`

Don't specify `:each`/`:example` scope for `before`/`after`/`around` blocks, as it is the default.

```ruby
# bad
describe '#summary' do
  before(:each) do
    # ...
  end

  # ...
end

# good
describe '#summary' do
  before do
    # ...
  end

  # ...
end
```

### Instance Variables

Use `let` definitions instead of instance variables.

```ruby
# bad
before { @name = 'John Wayne' }

it 'reverses a name' do
  expect(reverser.reverse(@name)).to eq('enyaW nhoJ')
end

# good
let(:name) { 'John Wayne' }

it 'reverses a name' do
  expect(reverser.reverse(name)).to eq('enyaW nhoJ')
end
```

### Empty lines

- Group `let`, `subject` blocks and separate them from `before`/`after` blocks.
- Leave one empty line between `feature`, `context` or `describe` blocks.
- Leave one empty line around `it` blocks. This helps to separate the expectations from their conditional logic (contexts for instance).

```ruby
# bad
describe Article do
  subject { FactoryBot.create(:some_article) }
  let(:user) { FactoryBot.create(:user) }
  before do
    # ...
  end
  after do
    # ...
  end
  describe '#summary' do
    it 'something' do
    end
    it 'something' do
    end
  end
  describe '#summary' do
    it 'something' do
    end
    it 'something' do
    end
  end
end

# good
describe Article do
  subject { FactoryBot.create(:some_article) }
  let(:user) { FactoryBot.create(:user) }

  before do
    # ...
  end

  after do
    # ...
  end

  describe '#summary' do
    it 'something' do
    end

    it 'something' do
    end
  end

  describe '#summary' do
    it 'something' do
    end

    it 'something' do
    end
  end
end
```

### Single expectation test

The 'one expectation' tip is more broadly expressed as 'each test should make only one assertion'.
This helps you on finding possible errors, going directly to the failing test, and to make your code readable.

Except for tests that are not isolated: feature specs, mainly the ones that use JS; and services that make requests to external APIs.
Specs that just use the database do not fall into this exception.

```ruby
# bad
it 'does the thing' do
  expect(service.call).to be_truthy
  expect(Thing.last.done?).to be_truthy
end

# good
it { is_expected.to respond_with_content_type(:json) }
it { is_expected.to assign_to(:resource) }

# good (not isolated)
it 'does the thing' do
  click_on "Do it"
  expect(Thing.last.done?).to be_truthy
  click_on "Undo it"
  expect(Thing.last.done?).to be_falsy
end
```

### Needed Data
Do not load more data than needed to test your code.

```ruby
# good
RSpec.describe User do
  describe ".top" do
    subject { described_class.top(2) }

    before { FactoryBot.create_list(:user, 3) }

    it { is_expected.to have(2).items }
  end
end
```

### Use `expect` instead of `should` syntax
On new projects always use the expect syntax.

``` ruby
# BAD

it 'creates a resource' do
  response.should respond_with_content_type(:json)
end

# GOOD

it 'creates a resource' do
  expect(response).to respond_with_content_type(:json)
end
```

### Use contexts
Contexts are a powerful method to make your tests clear and well organized. In the long term this practice will keep tests easy to read.

```ruby
# BAD
it 'has 200 status code if logged in' do
  expect(response).to respond_with 200
end

it 'has 401 status code if not logged in' do
  expect(response).to respond_with 401
end

# GOOD
context 'when logged in' do
  it { is_expected.to respond_with 200 }
end

context 'when logged out' do
  it { is_expected.to respond_with 401 }
end
```

### Example Descriptions
`it` block descriptions should never end with a conditional. This is a code smell that the it most likely needs to be wrapped in a context.

```ruby
# bad
it 'returns the display name if it is present' do
  # ...
end

# good
context 'when display name is present' do
  it 'returns the display name' do
    # ...
  end
end

# This encourages the addition of negative test cases that might have
# been overlooked
context 'when display name is not present' do
  it 'returns nil' do
    # ...
  end
end
```

### Expect a call to change something
Prefer `expect { ... }.to change { ... }.by(x)` syntax.

```ruby
# bad
it 'publishes the article' do
  article.publish

  expect(Article.count).to eq(2)
end

# bad
it 'publishes the article' do
  expect { article.publish }.to change(Article, :count).by(1)
end

# good
it 'publishes the article' do
  expect { article.publish }.to change { Article.count }.by(1)
end
```

### Shared Examples
Use shared examples to reduce code duplication.

```ruby
# bad
describe 'GET /articles' do
  let(:article) { FactoryBot.create(:article, owner: owner) }

  before { page.driver.get '/articles' }

  context 'when user is the owner' do
    let(:user) { owner }

    it 'shows all owned articles' do
      expect(page.status_code).to be(200)
      contains_resource resource
    end
  end

  context 'when user is an admin' do
    let(:user) { FactoryBot.create(:user, :admin) }

    it 'shows all resources' do
      expect(page.status_code).to be(200)
      contains_resource resource
    end
  end
end

# good
describe 'GET /articles' do
  let(:article) { FactoryBot.create(:article, owner: owner) }

  before { page.driver.get '/articles' }

  shared_examples 'shows articles' do
    it 'shows all related articles' do
      expect(page.status_code).to be(200)
      contains_resource resource
    end
  end

  context 'when user is the owner' do
    let(:user) { owner }

    include_examples 'shows articles'
  end

  context 'when user is an admin' do
    let(:user) { FactoryBot.create(:user, :admin) }

    include_examples 'shows articles'
  end
end

# good
describe 'GET /devices' do
  let(:resource) { FactoryBot.create(:device, created_from: user) }

  it_behaves_like 'a listable resource'
  it_behaves_like 'a paginable resource'
  it_behaves_like 'a searchable resource'
  it_behaves_like 'a filterable list'
end
```


### Leading subject
When subject is used, it should be the first declaration in the example group.

```ruby
# bad
describe Article do
  before do
    # ...
  end

  let(:user) { FactoryBot.create(:user) }
  subject { FactoryBot.create(:some_article) }

  describe '#summary' do
    # ...
  end
end

# good
describe Article do
  subject { FactoryBot.create(:some_article) }
  let(:user) { FactoryBot.create(:user) }

  before do
    # ...
  end

  describe '#summary' do
    # ...
  end
end
```
