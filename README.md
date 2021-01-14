<h1>---- RSpec Crib Sheet ----</h1>

<ul>
<li>Examples of basic syntax that's common in RSpec tests.</li>
<li>List is in alphabetical order</li>
<li>CAPITALISED sections elaborate or provide examples of particular types of test</li>
</ul>

**allow**

in below example, '':storm' randomly returns true or false; 'allow' forces false for the test

```rb
allow(subject).to receive(:storm) { false }

```


**be_an**

```rb
expect(subject.balance).to be_an(Numeric)
```

```rb
expect(subject.release_bike).to be_an_instance_of Bike
```

**before**

Use 'before' within 'Context' to limit its scope

```rb
before do
  subject.top_up(10)
end
```

**change**
```rb
expect { subject.touch_out }.to change{ subject.balance }.by(-1)
```

**CONSTANTS**

Syntax for using a constant in RSpec: ClassName::CONSTANT_NAME

```rb
expect { card.top_up(1) }.to raise_error "Card limit of £#{OysterCard::CARD_LIMIT} reached"

```

**DOUBLES**

```rb
let(:station) { double :station }
```

**eq**
```rb
expect(actual).to eq(expected)
```


**include**

```rb
expect(subject.runway).to include(plane)
expect(subject.runway).not_to include(plane)
```

**PREDICATE MATCHERS**

Predicate methods must: return a boolean value; and have a name that ends with ?
eg: method below is in_journey?. It returns True or False.

```rb
expect(subject).to be_in_journey
expect(subject).not_to be_in_journey
```

**raise_error**
```rb
expect { card.top_up(1) }.to raise_error "Card limit of £90 reached"
```

**RANDOMISATION TESTS**

Randomisation is tricky to test for in RSpec.
In the example below: <ul><li>dice.roll is a method that generates a random number between 1 and 6.</li>
<li>The result is stored in an array called 'roll'.</li>
<li>The test does not check whether dice_roll is random.</li>
<li>Instead, it checks if the 'expected' results in 'roll' correspond with an 'actual' real-world outcome
(eg, after 100 rolls we would expect the lowest number rolled to be 1 and the highest to be 6)</li></ul>

```rb
it "generates random numbers from 1 to 6" do
  dice = DiceRoller.new
  roll = dice.roll(100)
  actual = roll.minmax
  expected = [1,6]
  expect(actual).to eq(expected)
end
```
source: http://www.emilyplatzer.com/2014/04/21/basic-ruby-rspec.html

**respond_to**
```rb
it { is_expected.to respond_to(:method) }
it { is_expected.to respond_to(:touch_in).with(1).argument }
```
