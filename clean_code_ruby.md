# Clean Code The Ruby Way
#### By Logan Kane, Software Engineer Co-op at Rise People Inc

I recently finished reading `Clean Code by Robert C. Martin` [1]. Uncle Bob knows best, but his examples are in Java. The knowledge gained from this book can be applied to any programming language. Some things like naming or formatting have a certain way that a Rubyist would do it. Most use Rubocop for linting and formatting, and naming in Ruby follows a different convention than Java. Let’s adapt everything for Ruby!

I won’t touch on everything covered in Clean Code, but I will do variables, methods, objects, classes, and a few extras.
Things like formatting, error handling,  and comments are all preferential in how you or your organization chooses to handle them.

## Variables
> Variable paragraph

#### Use variables that have names which convey the meaning of what they are
``` Ruby
# Good


# Not so good

```

## Methods
> In Ruby, because everything is an object, there aren't functions, only methods. Methods are pieces of code that are associated with an object. This also means that Ruby is behaviour driven, rather than data driven. There isn't a large difference between a method and a function outside of that.

#### Something
``` Ruby
# Good


# Not so good
```

## Classes + Objects
> I'm lumping objects in with classes, because of the fact that everything is an object in Ruby, and I believe the advice pairs best here. 

#### Something
``` Ruby
# Good


# Not so good
```

Side note: What's a PORO (Plain Old Ruby Object)? Because everything is an object, doesn't that make PORO moot? Normally this is used when talking Rails, to differentiate between complex objects like an ActiveRecord model. Rails objects usually have complex logic or behaviour, which means that PORO is the differentiator for `simple`.

## Code Smells
> There are a bunch of code smells that Uncle Bob mentions, where he compiles a list from `Refactoring by Martin Fowler` [2]. Here are just a few of them.

#### Comments
Write concise, informative comments, making sure to delete them if obsolete, or if the code tells all of the information.
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
> I think most people are guilty of this at some point. DRY is important, but sometimes unavoidable.
``` Ruby
# Good, reusable
def add(a,b)
  a + b
end

# Not so good
def add5(a)
  a + 5
end
# OR
def add10(a)
  a + 10
end

...
```

#### Dead Code
> This is code that never gets reached. For some reason or another, this code isn't executed.
``` Ruby
case glass_level_percentage
  when 0
    ...
  when 25
    ...
  when 50
    ...
  when 75
    ...
  when 100
    ...
  when 110 # Oops, this won't be executed.
    ...
end
```

#### Avoid Negative Conditionals
> It is easier to understand positive logic over negative logic
``` Ruby
# Good
if employee_clock.tick

# Not so good (Basic, but still)
if !employee_clock.tick
```

## Extras 
> If you want another great book to read, try `Practical Object-Oriented Design in Ruby by Sandi Metz` [3].
- In Ruby, everything is pass by value, but these values are references to objects
- For formatting, you could use Rubocop with default rules. Easy!
- For error handling, use a service such as Airbrake, Sentry, Honeybadger, etc. They all have their own implementation.
- For comments, there should be an organization style guide for what constitutes a good comment.

## References/ Ruby Books
- [1] Clean Code by Robert C. Martin
- [3] Refactoring by Martin Fowler
- [2] Practical Object-Oriented Design in Ruby by Sandi Metz
