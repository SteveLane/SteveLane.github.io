---
layout: post
title: "Majority rules: counting a winner"
comments: true
tags: voting R
---

Most of us have had to vote at some stage: in primary/high school, perhaps to
elect class/school captains, during university to choose the best presentation
in your physics class, and obviously if you're old enough, voting in elections
for state/country leaders.

In Australia, we use
[preferential voting](http://en.wikipedia.org/wiki/Ranked_voting_system) to
elect officials, and for the lower house (House of Representatives), counting is
done using a full preferential system, also known as instant runoff voting
(IRV).

That's all well and good, and you can read up more about preferential voting at
the linked Wikipedia page, but why am I discussing voting? Last week was Barwon
Health Research Week, of which I was on the organising committee, and also one
of the poster judges. Research Week is an annual event at Barwon Health, which
aims to highlight all of the fantastic research done by Barwon Health and Deakin
researchers and staff.

As part of the poster judging, we also awarded a prize to the best 'Early Career
Researcher' (ECR) poster. There were nine judges at the session, and each of us
ranked a shortlist of five posters: preferential voting at its best!

When it came time to count the votes, there was not a clear winner (actually,
there was after looking at the data afterwards, but it didn't make a
difference!), so the question became how to decide on the winner? The chosen
method: sum the preferences for each poster, with the poster that had the
*smallest* number of total preferences being the winner.

As a statistician, this irked me. We had data in the form of ranks, but were
treating them as continuous data. Just because two of the judges placed poster A
above poster B, doesn't mean the difference between the two posters was judged
the same, rather that both judges *preferred* poster A to poster B.

Summing, or taking the mean of the preferences, is known as the
[Borda count](http://en.wikipedia.org/wiki/Borda_count), and by the description
of how it's done (mean/sum), you can see that it is an *average* method: the
candidate that wins the vote is often the consensus view, not that which is
preferred by the majority.

So what other methods could we use? The preferential method as described above?
Or the [Condorcet method](http://en.wikipedia.org/wiki/Condorcet_method), which
is a method that chooses the candidate that would win by majority against
pairings with all the other candidates. The Condorcet method is a *majoritan*
method. Unfortunately it doesn't work, because you can get cycles. A great
analogy is on the previously linked Wikipedia page: there may be a situation
where each candidate wins against another, like in a rock-paper-scissors game.

So how do the methods compare for the earlier mentioned poster competition at
Barwon Health? Let's have a look! Firstly, I found some code to calculate both
the Borda and Condorcet winner
[here](http://www.r-bloggers.com/condorcet-ranking-and-rcpp/). And here's the
data:


```r
votes <- structure(list(ProjectNumber = c("A", "B", "C", "D", "E"),
                        A = c(1L, 3L, 2L, 4L, 5L), B = c(3L, 4L, 2L, 1L, 5L),
                        C = c(2L, 4L, 5L, 1L, 3L), D = c(2L, 4L, 1L, 3L, 5L),
                        E = c(3L, 4L, 5L, 2L, 1L), F = c(1L, 3L, 2L, 4L, 5L),
                        G = c(1L, 3L, 5L, 4L, 2L), H = c(3L, 2L, 5L, 4L, 1L),
                        I = c(4L, 1L, 5L, 2L, 3L)),
                   .Names = c("ProjectNumber", paste("J", 1:9, sep = "")),
				   class = "data.frame", row.names = c(NA, -5L))
```

Firstly, what's the Borda count winner?


```
##   Names Average Rank Position
## 1     A     2.222222        1
## 4     D     2.777778        2
## 2     B     3.111111        3
## 5     E     3.333333        4
## 3     C     3.555556        5
```

Poster A is the winner by the Borda count, follwed by Poster D. What if we do
the full preferential count? There were 9 judges, so after distributing
preferences, a candidate needs 5 votes to be declared a winner. I did this
manually, and came up with again, Poster A, followed by Poster D.

Finally, how about the Condorcet method? Recall this method counts pairwise
winners:

```
##   Name Rank    Method
## 1    A    1 Condorcet
## 2    B    2 Condorcet
## 3    D    3 Condorcet
## 4    E    4 Condorcet
## 5    C    5 Condorcet
```

So here again, Poster A is the winner, but now the runner-up is Poster B: that
is, in all pairwise elections, Poster B came out the winner more often than
Poster D.

As it turned out, looking at the data, Poster A had the most first preferences
anyway with three votes, so to keep it simple, we should have picked it anyway!
But what's interesting, is that while Posters D and E each had 2 first
preferences, they were ranked third and fourth respectively by the Condorcet
method: most people preferred other posters.

What if the preferences had been slightly different? Let's look at swapping two
preferences for a single judge: Judge 8 will now vote Poster D first, and Poster
E fourth:


```r
votes2 <- votes
votes2$J8[4] <- 1
votes2$J8[5] <- 4
```

The Borda method still places Poster A first, with Posters E and C swapping
places:


```
##   Names Average Rank Position
## 1     A     2.222222        1
## 4     D     2.444444        2
## 2     B     3.111111        3
## 3     C     3.555556        4
## 5     E     3.666667        5
```

Most importantly though, the Concordet method now chooses Poster D as the
winner, with Poster A coming second!


```
##   Name Rank    Method
## 1    D    1 Condorcet
## 2    A    2 Condorcet
## 3    B    3 Condorcet
## 4    E    4 Condorcet
## 5    C    5 Condorcet
```

So whilst Posters A and D have the same number of first preferences, more people
preference D over all other posters, than they do A.

Above all else, congratulations to Poster A, which was produced by Dr Gemma
Vincent. Gemma scooped the pool at Research Week, winning another two prizes on
top of here ECR prize. Congratulations Gemma!

Majority rules!
