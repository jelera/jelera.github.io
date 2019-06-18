---
layout: post
title: "Why You Should Know About grep and Use an Alternative if you write programs"
description: "grep is a fantastic piece of software, but there are better options for developers"
date: 2019-05-31 12:00:31 -0500
tags: [ "Good Practice", "Programming Skills", "grep"]
# featured_image_thumbnail:
featured_image: assets/images/posts/2019/05/featured/grep.png
featured: true
# categories: "Text Editor", "Tool Setup", "Good Practice", "Ruby", "Python", "Vim", "Atom"
---
## A little Background

In the inception of UNIX, there were three initial core programs to make
everything work: a compiler (i.e [gcc](https://en.wikipedia.org/wiki/GNU_Compiler_Collection)), a shell (i.e. [bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell))), and an editor (i.e. [ed](https://en.wikipedia.org/wiki/Ed_(text_editor))).

Being developed in the 70's, meant that computational resources were very limited, with RAM reaching few tenths of KiloBytes, **`ed`** was the line editor, you read it right, `ed` operates line by line by default. This editor uses a clever command mode that allows user to maximize their experience by concatenating a set of numbers and mnemonic commands. For example, we wanted to:

- **Print** the ***5th line*** of a text file: `5p`
- **Print** the ***all the lines***: `1,$p`
- From the ***1st to the 4th line***, globally **search** for a *regular expression* and **delete** those matching lines: `(1,4)g/re/d`

## What is grep?

<a data-flickr-embed="true" data-footer="true"  href="https://www.flickr.com/photos/dannyman/9442491" title="GREP"><img src="https://live.staticflickr.com/5/9442491_f718b41e21_b.jpg" width="1024" height="768" alt="GREP"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

One evening, the original `ed` developer, [**Ken Thompson**](https://en.wikipedia.org/wiki/Ken_Thompson) was having a conversation with [**Lee McMahon**](https://en.wikipedia.org/wiki/Lee_E._McMahon), when the latter was interested in **finding occurrences of an arbitrary word** in [**The Federalist Papers**](https://en.wikipedia.org/wiki/The_Federalist_Papers), written under the pseudonym ***Publius*** by [Alexander Hamilton](https://en.wikipedia.org/wiki/Alexander_Hamilton), [James Madison](https://en.wikipedia.org/wiki/James_Madison) and [John Jay](https://en.wikipedia.org/wiki/John_Jay).

The [plain text file](http://www.gutenberg.org/cache/epub/18/pg18.txt) is 1.2 MegaBytes and since RAM was scarce, McMahon couldn't use `ed` to edit the file. That's when Ken Thompson wrote `grep` in one night using *PDP Assembly*, specializing the `g` **global command** from `ed`.

> Grep stands from `g/re/p` or **globally find** all the lines in a file or directory of files that matches the **RegEx** `/re/` and **print** them to stdout.

<iframe width="560" height="315" src="https://www.youtube.com/embed/NTfOnGZUZDk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 <p><a href="https://www.youtube.com/watch?v=NTfOnGZUZDk">Where GREP Came From</a> from <a href="https://www.youtube.com/channel/UC9-y-6csu5WGm29I7JiwpnA">Computerphile YouTube Channel</a> / <a href="https://en.wikipedia.org/wiki/Brian_Kernighan">Prof. Brian Kernighan</a> on <a href="https://youtube.com">YouTube</a>.</p>

## Rationale

As programmers, a big portion of a our career is **editing files**, and `grep` will ease the task of finding occurrences of functions, classes or variables in a project.

By simply using the command `grep -R some_function my_project `, we will get all the lines were `some_function` appears *recursively* in all the files inside the directory `my_project`.

The main issue with using `grep` in a modern development environment are all the files and folders that we don't want to include in our search; files like logs, `.vim` directories, logs, `tmp` files, etc.

While we can use option flags with `grep`, it gets out of hand really quick, and that's what when working with a development project directory, we should use other options.

## Alternatives

Thankfully there are many options for developers, tools that will respect the `.gitignore` file and will be optimized for the programming workflow.

### Ack

This program is written purely in Perl 5 and it takes advantage of Perl's naturally powerful text processing capabilities and regular expressions engine.

It is very portable as Perl runs almost everywhere.

### Ag, the Silver Searcher

According to the creator of `ag`, Geoff Greer, it is an "order of magnitude" faster than `ack`. It started as an `ack` clone but its features has diverged, making it a really fast solution.

We can also add more patterns to ignore in a `.ignore` file, such as `*.min.js` files. Also, `ag` is written on the **C language** and it's readily available in many operating systems.

[Ag: The Silver Searcher](https://geoff.greer.fm/ag/), [Source Code at Github](https://geoff.greer.fm/ag/).

### Sift, Grep on Steroids

Written in **Go**, `sift` claims to be even faster than `ag`, while also adding useful features for developers such as conditions, process inside gzipped files, search by file type, file extension, full path, file name, etc.

It also make it easier to ***Find and Replace*** without the use of other programs.

[Sift: Grep on Steroids](https://sift-tool.org), [Source Code at Github](https://github.com/svent/sift).

### Other Solutions

- [Pt, the Platinum Searcher](https://github.com/monochromegane/the_platinum_searcher).
- [Ripgrep](https://github.com/BurntSushi/ripgrep).

## Conclusion

Being aware of these programs will helps be more efficient in our workflow.

Cheers,
