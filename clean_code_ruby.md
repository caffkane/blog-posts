# Clean Code The Ruby Way
#### By Logan Kane, Software Engineer Co-op at Rise People Inc

I recently finished reading `Clean Code by Robert C. Martin` [1]. As they say, Uncle Bob knows best. Unfortunately, all his examples are in Java. The knowledge gained from this book can be applied to any programming language. Some things like naming or formatting have a certain way that a Rubyist would do it. Rubocop can be used for linting and formatting. Naming in Ruby follows a different convention than Java. Let’s adapt everything for Ruby!

I won’t touch on everything covered in Clean Code, but I will do variables, methods, objects, classes, and a few extras.
Things such as formatting, error handling, and comments are all user or organizational preferences.

## Variables
> Well named variables can be the difference between confusion and understanding. Misinterpreting what is going on in a method because of a poorly named variable isn't something you want.

#### Use intention revealing variable names AKA what they are
``` Ruby
# Good
admin_user = User.where(...)

# Not so good
u = User.where(...)

# This can get confusing if you're using multiple single letter variables, particularly in a loop or block.
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
## Methods
> In Ruby, because everything is an object, there aren't functions, only methods. Methods are pieces of code that are associated with an object. This also means that Ruby is behaviour driven, rather than data driven. There isn't a large difference between a method and a function outside of that.

#### Something
``` Ruby
# Good


# Not so good
```

#### Example 2
``` Ruby
# Good


# Not so good

```

#### Example 3
``` Ruby
# Good

# Not so good

```
## Classes + Objects
> Because everything is an object in Ruby, this advice pairs best with both classes and objects.

#### Something
``` Ruby
# Good


# Not so good
```

#### Example 2
``` Ruby
# Good


# Not so good

```

#### Example 3
``` Ruby
# Good

# Not so good

```
Side note: What's a PORO (Plain Old Ruby Object)? Because everything is an object, doesn't that make PORO moot? Normally this is used when talking Rails, to differentiate between complex objects like an ActiveRecord model. Rails objects usually have complex logic or behaviour, meaning PORO equates to `simple`.

## Code Smells
> Uncle Bob mentions a bunch of code smells, compiled from `Refactoring by Martin Fowler` [2]. Here are a few notable ones.

#### Comments
> Write concise, informative comments. Remove a comment when it is obsolete, or telling the same story the code tells.
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
> Most people are guilty of this at some point. DRY is important, but sometimes unavoidable.
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
  when 110 # Oops, this won't execute.
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
<!-- - In Ruby, everything is pass by value, but these values are references to objects  NOT NEEDED -->
- For formatting, you could use Rubocop with default rules. Easy!
- Exception handling services such as Airbrake or HoneyBadger, are useful for anything related to application errors.
- Organization style guides help with cohesion and what forms a good comment.

## References/ Ruby Books
- [1] Clean Code by Robert C. Martin
- [2] Refactoring by Martin Fowler
- [3] Practical Object-Oriented Design in Ruby by Sandi Metz
