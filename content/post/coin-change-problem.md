---
title: "Coin Change Problem"
date: 2017-12-28T13:57:10-02:00
draft: false
tags: [algorithms, dynamic programming]
summary: Determine the number of ways of making change for c units, using the given types of notes/coins.
---

You went to a restaurant and now you have to pay the bill. 
After making the payment, you need to receive a \$ 30 change. 
Knowing that the restaurant has an infinite amount of \$ 1, 
\$ 2, \$ 5, \$ 10 and \$ 20 notes, 
how many note combinations can you receive 
for this change?

As you can see, there are several possible combinations, for example:

- 10, 10, 10
- 20, 10
- 20, 5, 5
- 10, 10, 5, 5

First, let's define the variables that will be used in this problem.

- ```c```: change. Ex: 30
- ```n```: total number of notes. Ex: 5
- ```notes```: an array containing the notes. Ex: (1, 2, 5, 10, 20)

We can assume that:
 
- All variables will be storing positive integers, or a list of them.
- Notes can be an unsorted list.
- There can be a note that's bigger than the change value.

As you can probably figure out we'll have to loop over the notes array to find the possible combinations for the given change.

However, after we do that, we'll divide the problem into 
sub-problems. For checking how many change combinations can 
be made using the note \$ 5, for example, we'll have to calculate 
how many possible combinations can be made for the change $ 25.

As you can see this is a recursive problem, 
in which each note will have to calculate the total combinations 
for the resulting value of ``` c - note ```. The sum of the results 
of this process for all of the notes will give us the answer.

Now for the implementation, there's many possible algorithms for 
this problem, I'll use here an iterative one with a complexity of 
Θ(n*m) for the running time and Θ(n) for the storage usage.

{{< highlight python >}}
c, n = 30, 5
notes = [1, 2, 5, 10, 20]
combinations = [1]+[0]*c
for note in notes:
    for j in range(note, c+1):
        combinations[j] += combinations[j-note]
print(combinations[c]) #109
{{< /highlight >}}

This algorithm creates a list with all of the possible 
combinations from (0...c), the last entry, 
contains the answer we are looking  for.

If for some reason we'd need to re-calculate for a change of \$ 25, 
we can simply return what's stored on the index 25 
of the combinations array, since that already contains 
the result for this number.
