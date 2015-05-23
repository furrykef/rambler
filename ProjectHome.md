**Rambler** is a system for generating text. It is similar in principle to systems such as the [Dada Engine](http://dev.null.org/dadaengine/) (which powers the famous Postmodern Thesis Generator) and [rmutt](http://www.schneertz.com/rmutt/), but it is focused more on being friendly to writers while not sacrificing power. Grammars for Rambler are generally built on [YAML](http://yaml.org/) rather than a BNF-like notation.

The following is a simple Rambler script:
```
%YAML 1.1
---
toplevel:
- "[hello], [world]!"

hello:
- "Hello"
- "Greetings"
- "Salutations"

world:
- "world"
- "galaxy"
- "universe"
```

When this script is run, it will print one of "Hello, world!", "Greetings, galaxy!", "Hello, universe!", etc.

You can use Rambler to generate slight variations based on a rigid structure or wildly varying screeds. You can use it to generate news headlines, stories, or profane rants. You can use it on the web, in video games, or for your private amusement. The only limit is your imagination!