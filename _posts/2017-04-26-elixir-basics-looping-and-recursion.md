---
layout: post
title: "Elixir Basics: Looping and Recursion"
date: 2017-04-26
category: programming
---

When I first started learning Elixir a couple years ago, recursion was not something I was using on a day-to-day basis. But the functional nature of Elixir forced me to learn the concepts and I thought I would share some of my findings.

## An Example Not in Elixir

As an example, lets find the minimum value in a list of numbers. A very simple approach in a language like C# could look something like this:

```csharp
int[] numbers = new int[] { 11, 4, 19, 18, 6, 5, 24, 8, 4 };
int min = numbers[0];

for (int i = 0; i < numbers.Length; i++)
{
    if (numbers[i] < min)
    {
        min = numbers[i];
    }
}

return min;
```

Now how would we accomplish something similar in Elixir? The first thing you will realize is that there is no `for` loop in Elixir. And since we will not have mutable state outside of our "loop", we will need a way to keep track of the state.

## Elixir Example

If you've read through the [Elixir guides](https://elixir-lang.org/getting-started/introduction.html), you'll find that [recursion](https://elixir-lang.org/getting-started/recursion.html) is the way to solve this in Elixir.

So lets start with a basic [`List`](https://hexdocs.pm/elixir/List.html) in Elixir:

```elixir
numbers = [ 11, 4, 19, 18, 6, 5, 24, 8, 4 ]
```

Now lets create a public `min/1` function to take in the list of numbers and some private functions that will be used to iterate over each item in the collection.

*Note: I am leaving out some guard clauses and validation in favor of simplicity for this post.*

```elixir
def min(numbers) do
  min(numbers, hd(numbers))
end

defp min([head | tail], min) when min <= head do
  min(tail, min)
end

defp min([head | tail], min) when min > head do
  min(tail, head)
end

defp min([], min) do
  min
end
```

The first function is public, and accepts the list of numbers and proceeds to call `min/2` passing the list as well as the first item in the list as the starting "min" value:

```elixir
def min(numbers) do
  min(numbers, hd(numbers))
end
```

[`hd/1`](https://hexdocs.pm/elixir/Kernel.html#hd/1) is an easy way to get the first item, or "head" of a list.

Next we have two functions that pattern match on a list using `[head | tail]` as the first argument as well as keeping track of the current "min" value as we go.

```elixir
defp min([head | tail], min) when min <= head do
  # Pass the rest of the list to the next iteration and since the min value
  # didn't change we just keep the existing min value
  min(tail, min)
end

defp min([head | tail], min) when min > head do
  # We encountered a new min value so we take the new value and set 
  # the current state (the "min" argument) to the current head
  min(tail, head)
end
```

The guard clauses on the functions ensure that the correct function gets called depending on if we encounter a new minimum value, thus resetting the `min` variable and passing it along to the next call.

The last function pattern matches on an empty list:

```elixir
defp min([], min) do
  min
end
```

This tells us that we have reached the end of the list and there are no further items to iterate over. We simply return the current `min` value and the recursion has come to an end.

At this point we end up with `4` being returned as the min value from our original list.

## Tail Call Optimization

Erlang includes a nifty optimization for tail recursion that will help us with large lists. As explained in the [excellent post by Phillip Brown about Tail Call Optimization](https://www.culttt.com/2016/06/06/understanding-recursion-tail-call-optimisation-elixir/):

> Tall Call Optimisation is where if the last thing a function does is call another function, the compiler can jump to the other function and then back again without allocating any additional memory.

As you can see in the code above we are taking advantage of this optimization, so we should not run into any memory issues with large lists of numbers.

## Closing Thoughts

There are other ways a "min" function could be written. For instance, similar algorithms could be solved using the `map` or `reduce` functions in the [Enum](https://hexdocs.pm/elixir/Enum.html) module built into Elixir; but that is a topic for a future post. For now, I wanted to show how to implement something simple using recursion, and I hope this post will help you.

You can pull this example and others (along with tests) from the following repo: [https://github.com/mkchandler/MathFunctionsElixir](https://github.com/mkchandler/MathFunctionsElixir)
