# Clean Code The Ruby Way
#### By Logan Kane, Software Engineer Co-op at Rise People Inc - Updated March xxth, 2020

I recently finished reading `Clean Code by Robert C. Martin` [1].
As they say, Uncle Bob knows best. Unfortunately, all his examples are in Java.
The knowledge gained from this book can be applied to any programming language.
Some things like naming or formatting have a certain way that a Rubyist would do it.
Rubocop can be used for linting and formatting.
Naming in Ruby follows a different convention than Java. Let’s adapt everything for Ruby!

I'm going to be touching on core pieces of what is covered in Clean Code,
including variables, methods, objects, classes, and a few extras.
Things such as formatting, error handling, and comments are all user or organizational preferences.

## Variables
> Well named variables can be the difference between confusion and understanding.
Misinterpreting what is going on in a method because of a poorly named variable isn't something you want.

#### Use intention revealing variable names AKA what they are
``` Ruby
# Good
admin_user = User.where(...)

# Not so good
u = User.where(...)

# This can get confusing if you're using multiple
# single letter variables, particularly in
# a loop or block.
```

#### Avoid names that are misleading or confusing
``` Ruby
# Good
employee_time_off_events = Calendar.new

# Not so good
cal = Calendar.new
```

#### Avoid including the type in the name
``` Ruby
# Good
employee_phone_number = 555_555_5555

# Not so good
phone_number_int = 123_456_7890
```
## Methods + Functions
> In Ruby, because everything is an object, there aren't functions, only methods.
Methods are pieces of code that are associated with an object. This also means that Ruby is behaviour driven,
rather than data driven.

#### Limit Method Arguments (no more than 3)
``` Ruby
# Best (1 or 2)
def street_name_generator(num, string)
  num + string
end

# Good
def event_creator(date, location, name)
...
end

# Not so good, what kind of arguments is this
# going to be taking in?
def doing_lots(*args)
...
end

# This means that this method now has to do a lot
# Methods shouldn't be more than a few lines long
# This allows them to do one thing, and one thing well.
def doing_even_more(date, num, name, location)
...
end
```

#### Methods should do one thing
``` Ruby
# Good
def print_trophies(trophies)
  trophies.each do |trophy|
    puts trophy
  end
end

# Not so good, this does boolean logic, printing, and a method call
def active_sport_player_trophies(name, active, sport)
  if active
    player_trophies = get_sport_trophies(name, sport)
    player_trophies.each do |trophy|
      puts trophy
    end
  else
    puts "This player is not active."
  end
end
```

#### Methods should be small
``` Ruby
# The famous Rubyist Sandi Metz recommends 5 lines max
# I think 5 lines or less is a hard goal to hit but it
# means that your method is only doing one thing!
# It also means you extract logic to new methods

# Good
def thing_comparison(thing)
  if this == thing
    puts thing
  else
    puts "Not #{thing}"
  end
end

# Not so good
def return_of_the_thing(thing)


end
```
## Classes
> Everything is an object in Ruby. Classes included.
SOLID principles can be applied to a lot of the class advice given!

### Classes should be small - [Single Responsibility Principle (S in SOLID)]
``` Ruby
# Count responsibilities, not lines.
# Should you have everything piled on one desk?
# Or organize everything into filing cabinets?

# Good
Class ResourceMaker

end

# Not so good
Class ResourceMaker

end
```

#### Classes should be organized - [Open Close Principle (O in SOLID)]
``` Ruby
# Small, organized classes means that functions are less likely to break one another
# In this way, we can make sure that our class is OPEN for extension,
# but CLOSED for modification

# Good
Class ResourceMaker
  # Some code that is O
end

# Not so good
Class ResourceMaker
  # Some code that is not O
end
```

#### Classes should be - [Dependency Inversion Principle (D in SOLID)]
``` Ruby
# Abstract away classes from the concrete details.
# Abstract classes allow for easier testing and
# making sure nothing breaks when details change

# Good
Class ResourceMaker

end

# Not so good
Class ResourceMaker

end
```
Side note: Make sure not to abstract too early, or if needed at all.
An example of this is database adapters. Yes, it is possible to create an abstract adapter
so that you can make both a MongoDB adapter and a PostgreSQL adapter.
In reality, most use cases never warrant switching over to a new database client.
There is a reason that organizations still use MSSQL or Oracle after 30+ years.

#### Classes should be cohesive

``` Ruby
# Classes should touch as much of the variables as possible
# If they variables aren't used, split the class up
# If a class gets too long, extract methods to a resource

# Good
Class ResourceMaker

end

# Not so good
Class ResourceMaker

end
```

>Ruby Object Note: What's a PORO (Plain Old Ruby Object)?
Because everything is an object, doesn't that make PORO moot?
Normally this is used when talking Rails, to differentiate between complex objects
like an ActiveRecord model. Rails objects usually have complex logic
or behaviour, meaning PORO equates to `simple`.

## Code Smells
> Uncle Bob mentions a bunch of code smells, compiled from `Refactoring by Martin Fowler` [2].
Here are a few notable ones.

#### Comments
> Write concise, informative comments. Remove a comment when it is obsolete,
or telling the same story the code tells.
Here are some examples of bad comments:
``` Ruby
# This is the speak method for the ... class (Redundant)
def speak
  ...
end

# TODO: Refactor (Poorly Written)
def my_method
  ...
end

# We don't use this anymore because I said so (Commented Out Code)
# def unused_method
#   ...does this
#   ...then that
# end
```

#### Duplication
> Most people are guilty of this at some point. Don't Repeat Yourself (DRY) is important.
``` Ruby
# Good, reusable
def add(a,b)
  a + b
end

# Not so good
def add5(a)
  a + 5
end

# If we want to add a new number
# like 10, we have to duplicate
def add10(a)
  a + 10
end

... # And so on
```

#### Dead Code
> This is code that never gets reached. For some reason or another, this code isn't executed.
``` Ruby
case glass_level_percentage
  when 0
    puts "Empty"
  when 25
    puts "25% Full"
  when 50
    puts "50% Full"
  when 75
    puts "75% Full"
  when 100
    puts "100% Full"
  when 110 # Oops, this won't execute.
    puts "110% Full"
end
```

#### Avoid Negative Conditionals
> It's easier to understand positive logic over negative logic
``` Ruby
# Good
if employee_clock.tick

# Not so good (Basic, but still)
if !employee_clock.tick
```

## Extras
> If you want another great book to read, try `POODR by Sandi Metz` [3].
<!-- - In Ruby, everything is pass by value, but these values are references to objects  NOT NEEDED -->
- For formatting, you could use Rubocop with default rules. Easy!
- Exception handling services such as Airbrake or HoneyBadger, are useful for anything related to application errors.
- Organization style guides help with cohesion and what forms a good comment.

## References/Ruby Books
- [1] Clean Code by Robert C. Martin
- [2] Refactoring by Martin Fowler
- [3] Practical Object-Oriented Design in Ruby by Sandi Metz
