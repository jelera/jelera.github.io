---
layout: post
title: "Enumerable in Ruby: group_by and transform_values"
date: 2019-04-21 14:14:11 -0500
description: ""
categories: ruby programming enumerable collections howto
author: jose
---
In the beginning of my learning experience with Ruby at Flatiron School, I came
across an lab that was quite a challenge, **grouping items from an enumerable
and return a hash**, where the keys and values had been arranged in ordered
semantic way. After a hefty amount of Google searches, this premise was all too
common when working with collections, such as arrays or hashes.

![Boromir complains about iterating array of arrays](/assets/img/onedoesnotsimply-array_of_arrays.jpg)

Well, Boromir, like you, I let the influence of Isildur's Bane cloud my judgement, and succumb to despair. Well, not quite that dramatic, but it was indeed a daunting task.

In the beginning of my online research, I thought, while often occurring
problem, that would have involved a bunch of loops and hacky code that someone
had probably already made it into a gem.

Enter Matz...

>... then Matz took the best of list processing from Lisp, and the best of OO
>from Smalltalk and other languages, and the best of iterators from CLU, and
>pretty much the best of everything from everyone.
>
> &mdash; <cite>Steve Yegge</cite>

As in that quote, Ruby has a robust library in
[**Enumerate**](https://ruby-doc.org/core-2.6.3/Enumerable.html) that allows us
programmers to have granular control in how exactly we can process a collection
or any other enumerable, all in an elegant way.

## The Problem

While I don't exactly remember the exact details of the lab, the main challenge
was to **group two collections by an arbitrary parameter**, or as we can put it,
*"Group them by in a semantic way"*, and the answer in all those Google searches
was to use
[`#group_by`](https://ruby-doc.org/core-2.6.3/Enumerable.html#method-i-group_by)
built-in method.

The all-mighty `#group_by` method can be accessed by any enumerable, meaning
that if you want to arrange items, or keys or values in an arbitrary semantic
way, you totally can, and Ruby empowers you.

The documentation is very clear that, after calling `#group_by`, one must use
a code block. Inside of that block is what the method will use for the
*"rule"* on how to group the items and it **also** will use that line to
create a key for the output hash.

I know, it is a mouthful, but after playing with it in a REPL environment, it
all made sense, so I will show you a few examples.

## Demonstration

Again, these are not the same arrays or hashes from the lab, but from this
purpose, these examples will do just fine.

### Example 1

We are going to group an **array** of `rock_hits`, where every item is
**another array** which represents a *song*, and in which the first element
is a `rock_band` and the second is a `rock hit`. Remember that, by using
`#group_by`, the return object will be an **hash**.

```ruby
rock_hits = [
    ["Queen", "Bohemian Rhapsody"],
    ["Queen", "Don't Stop Me Now"],
    ["Queen", "Another One Bites the Dust"],
    ["Queen", "We Will Rock You"],
    ["Queen", "Somebody to Love"],
    ["Queen", "I Want To Break Free"],
    ["Metallica", "Nothing Else Matters"],
    ["Metallica", "Enter Sandman"],
    ["Metallica", "The Unforgiven"],
    ["Metallica", "One"],
    ["Guns N' Roses", "Paradise City"],
    ["Guns N' Roses", "November Rain"],
    ["Guns N' Roses", "Knockin' On Heaven's Door"],
    ["Guns N' Roses", "Don't Cry"],
    ["Guns N' Roses", "Welcome to the Jungle"],
    ["Guns N' Roses", "Sweet Child O'Mine"],
    ["Guns N' Roses", "You Could be Mine"],
    ["AC/DC","Thunderstruck"],
    ["AC/DC","Back In Black"],
    ["AC/DC","Shoot to Thrill"],
    ["AC/DC","Dirty Deeds Done Dirt Cheap"]
  ]
```

We want to use the artist, or the first item of the nested arrays, for the
keys. We can do that by running the following command in **irb** or **pry**:

```ruby
rock_hits.group_by { |song| song[0].itself }
```

You may be asking yourself, what is `#itself`? Well, it's a [kernel
method](https://ruby-doc.org/core-2.2.0/Object.html#method-i-itself) that makes
an object... return itself. I know, right?.

The returned hash looks like this:

```ruby
{"Queen"=>
  [["Queen", "Bohemian Rhapsody"],
   ["Queen", "Don't Stop Me Now"],
   ["Queen", "Another One Bites the Dust"],
   ["Queen", "We Will Rock You"],
   ["Queen", "Somebody to Love"],
   ["Queen", "I Want To Break Free"]],
 "Metallica"=>
  [["Metallica", "Nothing Else Matters"],
   ["Metallica", "Enter Sandman"],
   ["Metallica", "The Unforgiven"],
   ["Metallica", "One"]],
 "Guns N' Roses"=>
  [["Guns N' Roses", "Paradise City"],
   ["Guns N' Roses", "November Rain"],
   ["Guns N' Roses", "Knockin' On Heaven's Door"],
   ["Guns N' Roses", "Don't Cry"],
   ["Guns N' Roses", "Welcome to the Jungle"],
   ["Guns N' Roses", "Sweet Child O'Mine"],
   ["Guns N' Roses", "You Could be Mine"]],
 "AC/DC"=>
  [["AC/DC", "Thunderstruck"],
   ["AC/DC", "Back In Black"],
   ["AC/DC", "Shoot to Thrill"],
   ["AC/DC", "Dirty Deeds Done Dirt Cheap"]]}
```

One may notice that even though, we might have accomplished our objective,
the `String` of the Artist is the key of the hash, but it's not exactly what
was asked of us. Mmmm... well okay... Let's try again, what about this REPL
command:

```ruby
rock_hits.group_by { |song| song.shift }
```

will return ...

```ruby
{
  "Queen"=>
  [["Bohemian Rhapsody"],
   ["Don't Stop Me Now"],
   ["Another One Bites the Dust"],
   ["We Will Rock You"],
   ["Somebody to Love"],
   ["I Want To Break Free"]],
 "Metallica"=>[["Nothing Else Matters"], ["Enter Sandman"], ["The Unforgiven"], ["One"]],
 "Guns N' Roses"=>
  [["Paradise City"],
   ["November Rain"],
   ["Knockin' On Heaven's Door"],
   ["Don't Cry"],
   ["Welcome to the Jungle"],
   ["Sweet Child O'Mine"],
   ["You Could be Mine"]],
 "AC/DC"=>
  [["Thunderstruck"], ["Back In Black"], ["Shoot to Thrill"], ["Dirty Deeds Done Dirt Cheap"]]}
```

We are almost there, but we can see that the values of the returned array is
a bunch of nested arrays. Like I said, we are almost there and we will take
it there!

It seems we need to **flatten** the values? `Array#flatten` will serve that
purpose. Now, we would have to iterate through every single array to flatten
it.

We have a [Ruby way](https://www.infoq.com/articles/what-is-the-ruby-way) of
doing this, all without using `#each`!

**[`Hash#transform_values`](https://ruby-doc.org/core-2.6.1/Hash.html#method-i-transform_values)
*to the rescue!**

![In a smash bros meme, Transform Values joins the battle](/assets/img/smashbros-transformvalues_joins.jpg)

When we read the documentation, it says that `#transform_values` takes a
`Hash` and it operates on its values. Pretty straight forward.

Let's go back to **irb**, and try:

```ruby
rock_hits.group_by { |song| song.shift }.transform_values { |values| values.flatten }
```

And, this is what we get in return.

```ruby
{
  "Queen"=>
  ["Bohemian Rhapsody",
   "Don't Stop Me Now",
   "Another One Bites the Dust",
   "We Will Rock You",
   "Somebody to Love",
   "I Want To Break Free"],
 "Metallica"=>
   ["Nothing Else Matters",
   "Enter Sandman",
   "The Unforgiven", "One"],
 "Guns N' Roses"=>
  ["Paradise City",
   "November Rain",
   "Knockin' On Heaven's Door",
   "Don't Cry",
   "Welcome to the Jungle",
   "Sweet Child O'Mine",
   "You Could be Mine"],
 "AC/DC"=>
  ["Thunderstruck",
   "Back In Black",
   "Shoot to Thrill",
   "Dirty Deeds Done Dirt Cheap"]
 }
```

**Eureka!**, this is the hash we were looking for!!!

#### Public Service Announcement:

> Remember that `Array#shift` is destructive, meaning that it will alter the
> original array. If you need to preserve the original array, you may need to
> make a copy of it.

### Example 2

Say we need to group an **array** of country names, by the first letter.

Having experience with `Enumerable#group_by` and `Hash#transform_values`, this
will be a piece cake.

```ruby
country_list =
["Afghanistan","Albania","Algeria","Andorra","Angola","Anguilla","Antigua
&amp;Barbuda","Argentina","Armenia","Aruba","Australia","Austria","Azerbaijan","Bahamas","Bahrain","Bangladesh","Barbados","Belarus","Belgium","Belize","Benin","Bermuda","Bhutan","Bolivia","Bosnia &amp; Herzegovina","Botswana","Brazil","British Virgin Islands","Brunei","Bulgaria","Burkina Faso","Burundi","Cambodia","Cameroon","Cape Verde","Cayman Islands","Chad","Chile","China","Colombia","Congo","Cook Islands","Costa Rica","Cote D Ivoire","Croatia","Cruise Ship","Cuba","Cyprus","Czech Republic","Denmark","Djibouti","Dominica","Dominican Republic","Ecuador","Egypt","El Salvador",...
```

We proceed with this command in your preferred REPL tool:

```ruby
country_list.group_by { |country_name| country_name[0].to_sym }
```

And, we get what we wanted ...

```ruby
{:A=>
  ["Afghanistan",
   "Albania",
   "Algeria",
   "Andorra",
   "Angola",
   "Anguilla",
   "Antigua &amp; Barbuda",
   "Argentina",
   "Armenia",
   "Aruba",
   "Australia",
   "Austria",
   "Azerbaijan"],
 :B=>
  ["Bahamas",
   "Bahrain",
   "Bangladesh",
   "Barbados",
   "Belarus",
   "Belgium",
   ....
```

I've used `#to_sym` to convert the string to a symbol as they then to be
better keys. I'll expand more on that in a later blog post.

We can even count how many countries there are, per letter. We will use our
old trusty `#transform_values`.

```ruby
country_list.group_by { |country_name| country_name[0].to_sym }.transform_values{ |values| values.count }
```

And the returned hash has the actual count of countries per letter.

```ruby
{:A=>13,
 :B=>19,
 :C=>17,
 :D=>4,
 :E=>6,
 :F=>7,
 :G=>15,
 :H=>4,
 :I=>9,
 :J=>4,
 :K=>4,
 :L=>9,
 :M=>18,
 :N=>10,
 :O=>1,
 :P=>10,
 :Q=>1,
 :R=>4,
 :S=>26,
 :T=>12,
 :U=>6,
 :V=>3,
 :Y=>1,
 :Z=>2}
```

### Example 3

In this example, we are going to group the *hash* by the keys `passed` and
`failed`. The score is goes from 0 to 100, where the student needs **at
least** 60 to pass.

Here we have a real-world example of the usefulness of `#group_by`. It is
possible that one day this method will come really handy and help you from
really hacky code.

Here is the `grades` hash.

```ruby
# The range of the grade are between 0 and 100
# At least 60 to pass, less and the student failed.

grades = {
  "Pedro" => 60,
  "Malik" => 59,
  "Penny" => 88,
  "Marissa" => 93,
  "John" => 75,
  "Juan" => 48,
  "Amy" => 75,
  "Sophia" => 35,
  "Carmen" => 79,
  "Mario" => 80,
  "Giovanni" => 60
}
```

Going to **irb**, let's run this code snippet.

```ruby
grades.group_by do |student_name, grade|
  grade >= 60 ? :passed : :failed
end
```

If you are not clear on the [ternary
operator](https://stackoverflow.com/questions/4252936/how-do-i-use-the-conditional-operator-in-ruby),
it comes really handy for those clean one liners.

Here we are entering a condition, on whether if the grade is more than or equals
to 60, or less than, then the item is assigned to the proper key.

And, here is our finished hash:

```ruby
{
  :passed=>
  [
    ["Pedro", 60],
    ["Penny", 88],
    ["Marissa", 93],
    ["John", 75],
    ["Amy", 75],
    ["Carmen", 79],
    ["Mario", 80],
    ["Giovanni", 60]
  ],
  :failed=>
  [
    ["Malik", 59],
    ["Juan", 48],
    ["Sophia", 35]
  ]
}
```

## Conclusion

Like peanut butter and jelly, `Enumerable#group_by` and `Hash#transform_values`
go well together, and should be part of your repertoire as a developer. Once
I'll start diving into advanced JavaScript development, I'll search what is the
equivalent of these helpful methods.

Cheers.
