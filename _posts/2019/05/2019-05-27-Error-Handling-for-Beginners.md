---
layout: post
title: "JavaScript Error Handling for Beginners"
description: "Why should you care on error handling when programming"
date: 2019-05-27 17:51:20 -0500
tags: [ "Good Practice", "JavaScript", "Error Handling"]
# featured_image_thumbnail:
featured_image: assets/images/posts/2019/05/featured/clean_code_featured.jpg
featured: true
# categories: "Text Editor", "Tool Setup", "Good Practice", "Ruby", "Python", "Vim", "Atom"
---

## Why is it Important
Pobody's nerfect! Mistakes are made everyday. Small and insignificant or big
doozies, unhandled errors will come and haunt your nightmares.

![Pobody's nerfect](https://media.giphy.com/media/xT9IgH6tFP7dNVrQAw/giphy.gif)

In many cases, **these exceptions can be toxic**, meaning that they will
cascade to other part of the codebase, making debugging an infuriating and
frustrating task as well as a huge waste of effort and time.

When your code becomes the slight of complexity, it becomes error-prone, and
it is imperative as a developer to use **Error Handling**, also known as
[Exception Handling](https://en.wikipedia.org/wiki/Exception_handling) at
your disposal.

While you can use many debugging techniques to test for errors, **Error
Handling** will take advantage of standards streams.

## What are Standard Streams
Without getting into [technical
details](https://en.wikipedia.org/wiki/Standard_streams), basically there are three
streams:

![Pobody's nerfect](/assets/images/posts/2019/05/Stdstreams-notitle.svg)

### Standard Output (STDOUT)
*It is the stream where a program writes its output data. The program
requests data transfer with the write operation.*

Most of the time, it is in the command line interface, where programs print
text to the console.

```bash
$ whoami
```

If you are not familiar with the `whoami` command, it prints the current logged user.

```bash
$ rails routes
```
This one will print out to STDOUT the defined routes for a Ruby on Rails application.

### Standard Input (STDIN)
*It streams data (often text) going into a program. The program requests
data transfers by use of the read operation.*

```bash
$ cat /etc/hosts > ~/hosts
```

The `cat` program will print out **every line of text** of any file into STDOUT, but using `>` command, we can redirect the text stream to STDIN and save it in the file `~/hosts`.

```bash
$ ls -la ~ | head -5
```

Using then `|`, aka **pipe command**, we can pipe the text stream from `ls`
into the `head` command, which will take a argument of *how many lines from
the top* are needed, and they will be printed out via STDOUT. In the example
above, we are printing the first 5 lines from the text stream of `ls`.

```bash
$ rails routes > ~/routes
```

The `~/routes` file will contained the output of `rails routes`.

A more approachable example for Rails developers, where let's say we want to share the routes of our Rails application to a person who does not have access to the project source code or repository.

### Standard Error (STDERR)
*This stream is another output stream typically used by programs to output
error messages or diagnostics.*

If there is an error during the program runtime, very likely it will use
Standard Error.

```bash
$ sass index.scss index.css 2>&1 errors.log
```

This is the command line app for [Sass](https://sass-lang.com), it will take
a SASS file and pre-process it into a CSS file. Any errors will be redirected to
STDERR with `2>&1` into the `errors.log` file.

```bash
$ bundle install 2>&1 ~/errors
```

If you have programmed with Ruby and used Bundler, you are very likely to have encountered with version errors. You can redirected the STDERR output to a `~/errors` file, and share it with other peers.

## Why again is this important

Understanding Standard Streams will give access to the bigger picture when it comes to **Text Processing**, a fundamental skill of Web Development.


## Error Handling

Programming languages designers acknowledge the importance of Exception
Handling and to make use of the STDERR outputs. They have included may
built-in tools are out disposition We are going to tackle the very basics
of JavaScript Error Handling.

![Pobody's nerfect](/assets/images/posts/2019/05/taken_meme.png)

<!-- ![Pobody's nerfect](http://www.quickmeme.com/img/f7/f7bcb1766f25c4190cd9cad4e2fcb23975e316235107f6f45cfa9276f16f3e87.jpg) -->

## JavaScript Exceptions

JavaScript lets us handle errors in straightforward way. We are given 4
statements and an `Error` object.

### The Error Object
The `Error` object has a special purpose. It has 2 properties, a name and a message

```javascript
const customError = new Error({
  name: 'customError',
  message: 'This is a custom message'
  })

throw customError
```

### try

The `try` statement allows us to test for errors. If one is found, `try` will throw an error.

### catch

This statement will **catch** error object and allows us to handle it.

### throw

The `throw` statement, together with `new` and `Error` will help you create
new error objects. We can also take advantage of the [built-in error
objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
provided by JavaScript.

```javascript
throw new Error('Some helpful message for your peers/future-self')
```

### finally

What `finally` does is to run code regardless whether an exception was raised or not.

### Using them all together

```javascript
try {
  // Try to run this code, if an error is thrown, it will be 'catch' in the `catch` statement.
}
catch (err) {
  // err is the Error object raised if the code on the `try` statement failed somehow.

  // console.error() is preferred when handling errors.
  console.error(err.message)
}
finally {
  // This code will run, regardless of the outcome on `try` or `catch`
}
```

## Again, why?

So you need more proof, ok, no problem, here you go!

![Chrome console with Javascript Error](/assets/images/posts/2019/05/js_console_error.png)

And, also debugging be like...
![Chrome console with Javascript Error](/assets/images/posts/2019/05/debugging_murder.jpg)



## Conclusion

Use Exception Handling for your own sake, you will curse your past-self or person who didn't/forgot to implement it.

Cheers,
