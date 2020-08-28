---
layout: post
date: 2020-08-28
author: Jason Brown
title: Using The Right Tool
---
Most of the lessons here are rather obvious ones but I'll record them here anyway. A few months ago, I needed to set up dynamic DNS for a domain of mine on Google Domains. I looked around for existing scripts to accomplish this but was unsatisfied with the ones I found so I decided to [write my own](https://github.com/noUsernamesLef7/google-dynamic-dns). I ended up writing it as a Bash script because the server had it installed but lacked a Python interpreter. Judging that it would be better to save the disk space and indulge in some (misguided) minimalism I began writing. The first version wasn't pretty but worked fine. A few months later I found myself a bit bored and decided to spend some time messing with the script and revising it. In doing so, I found myself frequently regretting having written it as a Bash script.

### Why Bash Wasn't The Right Tool
First off, the script works as written. It does it's job. I found while revising however, that as soon as I wanted to do anything of any real complexity I could think of several ways to implement it in Python in a way that was more readable, more efficient, and in many cases less complicated.

#### Clunky Syntax
Bash is not known for it's elegant syntax. Many simple constructs like conditionals and loops require multiple commands or can be created and formatted in many ways. For example, a basic if-else statement:

```bash
if [[ test ]]
then
	do something
else
	do something else
fi
```

is often made somewhat less awkward by formatting it

```bash
if [[ test ]]; then
	do something
else
	do something else
fi
```

The equivalent Python is:

```python
if test:
	do something
else:
	do something else
```

In my first version readability wasn't much of an issue as it was small and didn't validate any of data loaded or responses received. When I decided to add validation it quickly became much more difficult to read and error prone.

#### Testing
It turns out that unit testing in Bash is actually kind of possible, just inconvenient and clunky. The first step in doing so is to break all the code into separate functions and then at the bottom of the script, stick an if statement that if it's not called with a \--test argument runs a main() function. The result of this is that we can write another script where we

```
source script.sh --test
```

and have all the functions load into our shell but not run any of them. Then we write test cases where we pass a certain value to each our functions and make sure they are behaving as expected.

It's fairly obvious that this is a hacky workaround and doing this kind of testing in Python is trivial in comparison.


### Lessons Learned
Bash scripts earn you minimalism points, but Python scripts let you keep your sanity and make it easier to expand on an idea later.
Also, don't get stuck with something just because you've invested some time in it.  Sunk cost fallacy and all that. Learn to accept when your idea was a bad one and move on.
