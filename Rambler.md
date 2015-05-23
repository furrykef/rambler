# Introduction #
Welcome to Rambler!

## YAML files ##
Rambler is built on [YAML](http://yaml.org/). If you don't know YAML, don't worry; the subset needed for basic usage of Rambler is small and very easy to learn. You don't need to know all of YAML to use Rambler, though it can help at times.

## The command-line tool ##

## The library ##
The Rambler library does not rely on YAML per se (though the command-line tool does) -- you could just as easily use JSON or some kind of XML, for example, but we don't recommend it because using JSON would be ugly and using XML would be _very_ ugly. Still, if you come up with a better framework than YAML (and if you do, by all means tell us!), you can use it right away because the Rambler library doesn't care where you got your data from so long as you pass in a dictionary of rules.

## Syntax ##
`[foo]` means "emit a randomly-chosen string under the rule `foo`".

By default, Rambler will not reuse items it has already used if possible. For example, `[foo] and [foo]` will _never_ produce, say, `spam and spam` unless `spam` is the only item under the rule `foo`. This produces more variety in the output and generally helps ensure that undesirable repetition does not occur. However, when a rule is used repeatedly and its list of items is short, this will cause a cycle. For instance, if `foo` is defined thus:

```
foo:
- "A"
- "B"
```

then `[foo] [foo] [foo] [foo] [foo] [foo]` will either print `A B A B A B` or `B A B A B A`, never something like `B B A B A A`. This is because Rambler shuffles the list of `foo`'s strings once before beginning processing and never reshuffles it. The hope is that you'll repeat rules infrequently enough, and your lists are long enough, that this situation either never occurs or is not very noticeable if it does.

`{foo|bar|baz}` means "emit a randomly chosen string out of `foo`, `bar`, or `baz`". Unlike with rule lookup, nothing is done to ensure that items are not chosen repetitively. Thus, `{foo|bar} {foo|bar} {foo|bar}` may well print `foo foo foo`, and it may well print `foo foo foo` again if the rule is invoked a second time.

`<% foo %>` executes a Python statement with `exec` and prints nothing. This is generally used for assignment of variables: `<% foo = bar() %>`. Note that any variables thus assigned are global within the script, so use them with care. We recommend writing your script such that few variables are needed; if you are adding many variables, question if they are actually improving the quality of your writing.

`<%= foo %>` prints the value of `foo`. For example, `1 + 1 is <%= 1 + 1 %>` will print the text `1 + 1 is 2`.

Allowing embedded Python with `<% %>` and `<%= %>` entails a security risk if you use it on an unknown script since Python's sandboxing is poor. Therefore we disallow it by default so that people aren't caught unaware by the security risk. Pass `allow_eval=True` to `ramble` to allow it.

## Tips ##
  * Don't use Python's `print` statement/function unless your intention is to print debug info to the console window.