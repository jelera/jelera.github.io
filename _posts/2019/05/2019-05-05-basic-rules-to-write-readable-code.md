---
layout: post
title: "Becoming better at programming: Basic rules to write readable code"
description: "Be an civic programmer and stick to your language of choice's conventions using editorconfig, style guides and linters."
date: 2019-05-05 18:38:42 -0500 
tags: [ "Good Practice", "Ruby", "JavaScript", "Python", "Text Editor" ]
# featured_image_thumbnail:
featured_image: assets/images/posts/2019/04/featured/ruby_group_by_featured.jpg
featured: true
# categories: "Text Editor", "Tool Setup", "Good Practice", "Ruby", "Python", "Vim", "Atom"
---

If you are just starting to write programs and very likely you are getting
the hang of your text editor of choice, then you may also find out that
keeping a tidy code and reformatting old messy text can be tedious and
involves removing your hands from the keyboard and reaching for the mouse
more often that anyone would like.

Fortunately during my Programming journey, I have gather some tips that will
be of help.

## Become an expert in your main tool

A developer's main tool is the humble **Text Editor**. In our careers, we
spend a huge percentage of our time with that piece of software.

![xkcd.com comic where programmer are debating on which editor is best](https://imgs.xkcd.com/comics/real_programmers.png)

As in this already classic [xkcd.com](https://xkcd.com/378/) comic, **real
programmmers know how to use their text editor**.

Not just how to open a file and type, but take your time to read the
documentation, watch videos, make an effort in making those keybindings an
instantaneous muscle-memory movement. Commands, plugins and every resource
you can find, make it part of your arsenal.

On which editor to use? Well... That is **enterily up to you**. While I'm
bias toward Vim; Atom, Visual Studio Code, Brackets, Notepad++, their main
purpose is take care of changing bytes in a text file; learning the advanced
functionality will pay huge dividends later on.

## Read the style guide

A programming language's style guide provides a series of guidelines on how
to format your code. Just like in English, or any other human language, there
is a governing set of grammatic rules that **must be followed** in order to
be understood by everyone else.

> All code in any code-base should look like a single person typed it, no
> matter how many people contributed.
>
>  &mdash; <cite>Source: <a href='https://codeburst.io/5-javascript-style-guides-including-airbnb-github-google-88cbc6b2b7aa'>codeburst.io</a></cite>

Like in graphic and UX design, getting acquainted with the style guide will
help you in building good habits in writing software. This comes specially
handy when you are starting to working with other developers.

One example that comes to mind is [Python's
PEP-8](https://www.python.org/dev/peps/pep-0008/). In Python, whitespace is
very important as the interpreter wouldn't run your program if your
indentation is off. PEP-8 is a great reference for every aspiring and
seasoned Python developer.

In JavaScript, there are many style guides, with the most popular ones being
from [AirBNB](https://github.com/airbnb/javascript),
[Google](https://google.github.io/styleguide/jsguide.html) and [JavaScript
Standard Style](https://github.com/standard/standard).

While Ruby's [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar)
gives developers a unique freedom to writing code, Rubyists have a thorough
resource in [Rubocop's Ruby Style
Guide](https://github.com/rubocop-hq/ruby-style-guide).

> This Ruby style guide recommends best practices so that real-world Ruby programmers can write code that can be maintained by other real-world Ruby programmers

By following these style guides, we will be compliant with other member of
the community, we make our code very readable to external readers and create
good habits, making you a competent developer.

# Use .editorconfig

In our careers, we are going to encounter other teammates or organizations
that uses a different text editor or IDE that what we are used to. It's not
uncommon to see some people prefering Emacs, or Sublime Text, or maybe and
IDE like RubyMine, as you might guess, configuring and setting each different
tool makes for a headache an a half.

![Mac vs PC parody image Tabs vs Spaces](/assets/images/posts/2019/05/tabs_v_spaces.png)

Well, Fear not as the [.editorconfig project](https://editorconfig.org/) is
an effort to consolidate the settings for formatting, indentation

Using a single text config file, your team/organization can set up everyone's tools with the agreed settings like whether to use spaces or tabs, and other idiosincracies that may cause the code produced to be irregular.

# Install linters and formatting helpers plugins

If you are not familiar with linters, they will either make your life easier or they will whine on how badly your code is formatted that it'll make you feel down, and many days they will do both.

> JSLint will hurt your feelings. Side effects may include headache, irritability, dizziness, snarkiness, stomach pain, defensiveness, dry mouth, cleaner code, and a reduced error rate.
>
>  &mdash; <cite>Douglas Crockford via the <a href='https://www.jslint.com/help.html'>JSLint site</a></cite>

A [linter](https://en.wikipedia.org/wiki/Lint_(software)) is a piece of
software that analyzes your code, and it gives you feedback about formatting
errors, suspcious constructs and even bugs.

If you enjoy programming in JavaScript, or maybe not enjoy, but at least you
don't go insane while writing in it, you may have to give a shoutout to
[Douglas Crockford](http://www.crockford.com/). During the times of the Web
2.0 and AJAX, Mr. Crockford authored a book called [JavaScript: The Good
Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford-dp-0596517742/dp/0596517742/ref=mt_paperback?_encoding=UTF8&me=&qid=),
which is an amazing book for when JavaScript was having even more terrible
reputation; he would say that *"JavaScript is a beautiful language if you
avoid the bad parts"*.

And to avoid those bad parts, he wrote [JSLint](https://www.jslint.com/) in which the program would shout at you if you are using said "bad parts" of the language, and as he puts it...

> JSLint was designed to reject code that some would consider to be **perfectly fine**. The reason for this is that JSLint's purpose is to help produce programs that are free of error. That is difficult in any language and is especially hard in JavaScript

By the way, Douglas is also the creator of JSON file format, so you don't have to be
dealing with crazy XML response files.

Python and Ruby also have linters, with the popular ones being [Flake8](http://flake8.pycqa.org/en/latest/) and
[Rubocop](https://docs.rubocop.org/en/latest/), respectively.

![Obi Wan Kenobi dealing with linters ](/assets/images/posts/2019/05/obi_wan_linter.jpg)

Maybe the question in your mind is *"How in the heck are you gonna be able to
use those linters together with your text editor"*.

Simple, **plugins**.

Good thing that programmers like to automatize every process
they can get their hands on and this is no exception. If you google "linters"
for your language plus your text editor, it is almost a safe bet that someone
has your back.

# Conclusion

Be an text editor Jedi, get familiar with the style guide of the language of your choice, and make use of linters to help you (hurt your feelings).

Now, I'm not going to go into *the text editor wars* or tell why editor X is
better than editor Y. Let's not waste our time, for we all can conclude that
... **Vim is the best editor**!

![Andy Dwyer is amazed](https://media.giphy.com/media/5VKbvrjxpVJCM/giphy.gif)
 (See what I did there, wink wink...).

 Cheers.
