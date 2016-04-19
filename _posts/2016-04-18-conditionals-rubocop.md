---
layout: post
title: Multi-line conditionals in Ruby
summary: Darn rubocop
---
I try my best to write syntactically idiomatic Ruby code in the first go. If I don't, `rubocop` makes sure to give me the stink eye. Most of the time, I subserviently agree with the mistakes it corrects and faux pas it points out, and I learn how to write prettier Ruby. Today, I had a double-take.

`rubocop` corrected my Chef resource guard from

```ruby
only_if do
  condition1 &&
  condition2 &&
  condition3 &&
  condition4
end
```

to

```ruby
only_if do
  condition1 &&
    condition2 &&
    condition3 &&
    condition4
end
```

I'm used to giving multi-line conditionals normal indentation treatment in other languages, and it reads pretty clearly to me. I can agree, in Ruby at least, that it helps with readability if there is code that follows the conditionals, like in [this example](https://github.com/bbatsov/ruby-style-guide/issues/476). Maybe `rubocop` just isn't fancy enough to detect that there isn't a following code block. Or maybe it's hinting that I should remodel the code as a state machine because it's angry at dealing with long conditionals.
