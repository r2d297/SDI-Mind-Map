WEBVTT

1
00:00:01.921 --> 00:00:04.734
In this video, we're going to look
at the concept of independence.

2
00:00:04.734 --> 00:00:08.734
Independence happens when the occurrence
of one event does not affect

3
00:00:08.734 --> 00:00:11.796
the probability of
the occurrence of another event.

4
00:00:11.796 --> 00:00:14.315
For example, if I toss a coin twice,

5
00:00:14.315 --> 00:00:20.021
whatever happened on the first throw does
not affect the outcome of the second one.

6
00:00:20.021 --> 00:00:22.531
On the other hand, if I'm playing chess,

7
00:00:22.531 --> 00:00:27.156
whatever happened on the 10th move
affects what happens on the 11th move.

8
00:00:27.156 --> 00:00:31.588
So these are not independent, but
the coin throws are independent.

9
00:00:31.588 --> 00:00:34.842
Understanding independent is very
important in probability and

10
00:00:34.842 --> 00:00:39.158
in machine learning, because assuming that
things are independent actually helps us

11
00:00:39.158 --> 00:00:41.539
simplify calculations and
make predictions.

12
00:00:41.539 --> 00:00:43.345
So let's calculate one more probability.

13
00:00:43.345 --> 00:00:48.252
In a school, there are 100 kids, half of
them so 50 of them like playing soccer,

14
00:00:48.252 --> 00:00:50.924
and the other half do
not like playing soccer.

15
00:00:50.924 --> 00:00:55.839
The kids are randomly split
into two equal rooms,

16
00:00:55.839 --> 00:00:58.773
each one of them of size 50.

17
00:00:58.773 --> 00:01:01.344
That's room 1 and room 2.

18
00:01:01.344 --> 00:01:04.618
So for this question, you're not
required to make any calculations.

19
00:01:04.618 --> 00:01:09.599
The question is, based on your knowledge,
what is your best

20
00:01:09.599 --> 00:01:15.078
estimate about the number of kids
in room 1 who would like soccer?

21
00:01:15.078 --> 00:01:20.200
And remember, the kids were randomly
split into two equally sized rooms.

22
00:01:20.200 --> 00:01:22.877
So the split will most
likely look as follows.

23
00:01:22.877 --> 00:01:26.767
Roughly 25 kids in the first
room will like soccer, and

24
00:01:26.767 --> 00:01:29.048
roughly 25 in the second room.

25
00:01:29.048 --> 00:01:33.924
Because they were randomly split,
there was no reason

26
00:01:33.924 --> 00:01:38.915
to go to room 1 versus room 2,
and so that is 25 each.

27
00:01:38.915 --> 00:01:43.796
Obviously, something different would have
happened, but our best estimate is 25.

28
00:01:43.796 --> 00:01:48.955
Because if roughly half of the kids play
soccer and they're split into two rooms

29
00:01:48.955 --> 00:01:53.975
half half, then roughly half of the kids
in each one of the rooms play soccer.

30
00:01:53.975 --> 00:01:58.378
Now, imagine another school with 100 kids,
but in this school only 40 of them like

31
00:01:58.378 --> 00:02:01.963
playing soccer, which means 60 of
them don't like playing soccer.

32
00:02:01.963 --> 00:02:07.638
The kids are randomly split into two size,
this time of different size,

33
00:02:07.638 --> 00:02:11.465
room 1 can fit 30 kids and
room 2, 70 kids.

34
00:02:11.465 --> 00:02:13.696
So, same question as before.

35
00:02:13.696 --> 00:02:15.425
Based on your knowledge,

36
00:02:15.425 --> 00:02:20.452
what is your best estimate about how
many kids in room 1, the smaller room,

37
00:02:20.452 --> 00:02:25.263
like to play soccer, or at least what
would you expect this number to be?

38
00:02:25.263 --> 00:02:28.989
Well, since the split is 40-60 for
soccer and not soccer,

39
00:02:28.989 --> 00:02:33.612
we expect that since we separated the kids
randomly, then in each of the rooms,

40
00:02:33.612 --> 00:02:35.966
the split is going to be 40-60 again.

41
00:02:35.966 --> 00:02:41.437
So we expect 40% of the kids
in room one two like soccer,

42
00:02:41.437 --> 00:02:47.478
and that's exactly 12 kids,
because 40% of 30 is 12.

43
00:02:47.478 --> 00:02:52.910
More clearly, we have 40% of 100 kids
playing soccer, that is 40 kids.

44
00:02:52.910 --> 00:02:56.406
And the probability of a kid
playing soccer is 0.4.

45
00:02:56.406 --> 00:03:01.099
And then there's 60 kids
who don't play soccer, so

46
00:03:01.099 --> 00:03:06.621
the probability of a kid not
playing soccer is 60% or 0.6.

47
00:03:06.621 --> 00:03:09.684
Now, we can split them into two rooms.

48
00:03:09.684 --> 00:03:12.165
There's 30% of the kids in room 1.

49
00:03:12.165 --> 00:03:15.209
So the probability of room 1 is 0.3.

50
00:03:15.209 --> 00:03:19.499
And the question is what is
the probability that a kid plays soccer and

51
00:03:19.499 --> 00:03:20.425
is in room 1?

52
00:03:20.425 --> 00:03:24.437
So we have P of soccer, which is 0.4,

53
00:03:24.437 --> 00:03:28.454
and P of R1, room 1, which is 0.3.

54
00:03:28.454 --> 00:03:31.637
And we're looking for
this probability over here.

55
00:03:31.637 --> 00:03:34.994
So probability of soccer,
intersection room 1.

56
00:03:34.994 --> 00:03:41.870
And as you can see, that the probability
of soccer times the probability

57
00:03:41.870 --> 00:03:47.179
of room 1 which is over here,
that's 0.4 x 0.3.

58
00:03:47.179 --> 00:03:51.317
In other words,
remember that we took 40% off 30%.

59
00:03:51.317 --> 00:03:55.798
That means we're multiplying them and
we get 12% or 0.12.

60
00:03:55.798 --> 00:03:59.275
What we're talking here is
the intersection of two events.

61
00:03:59.275 --> 00:04:01.864
When you see the word and
that's intersection.

62
00:04:01.864 --> 00:04:06.713
So the probability that a kids play
soccer and is in room 1 is because

63
00:04:06.713 --> 00:04:11.222
those events are not related,
are independent of each other,

64
00:04:11.222 --> 00:04:16.262
then it's the product of the two
probabilities P(S) and P(R1).

65
00:04:16.262 --> 00:04:18.598
So we get to the product rule.

66
00:04:18.598 --> 00:04:22.866
The product rule simply says probability
of a intersection B is probability

67
00:04:22.866 --> 00:04:24.673
of A times the probability of B.

68
00:04:24.673 --> 00:04:27.792
This is going to be very useful,
but remember, the events have

69
00:04:27.792 --> 00:04:31.413
to be independent and we're going to
see more details about this later.

70
00:04:31.413 --> 00:04:35.918
To continue illustrating the intersection
of independent events and

71
00:04:35.918 --> 00:04:40.510
the probability of that, we're going
to look at a coin example again.

72
00:04:40.510 --> 00:04:44.604
So let's consider tossing
a fair coin five times.

73
00:04:44.604 --> 00:04:46.167
Here's a question for you.

74
00:04:46.167 --> 00:04:51.547
What is the probability that the coin
lands in heads all five times?

75
00:04:51.547 --> 00:04:56.016
Well, note that each event is independent
from all the other ones because one coin

76
00:04:56.016 --> 00:04:59.015
landing in heads does not
affect any of the other ones.

77
00:04:59.015 --> 00:05:03.333
Therefore, the probability is
the probability of the first one lands in

78
00:05:03.333 --> 00:05:08.093
heads, which we know it's one half times
the same thing for all the other ones.

79
00:05:08.093 --> 00:05:12.386
So it's one half times one half times
one half times one half times one half.

80
00:05:12.386 --> 00:05:18.246
And that is going to be 1/32 because

81
00:05:18.246 --> 00:05:25.181
it's 1/2 to the five and that is 1/32.

82
00:05:25.181 --> 00:05:29.541
So this product rule can be extended,
it's not just two events.

83
00:05:29.541 --> 00:05:33.139
But if you have many independent events
all independent from each other,

84
00:05:33.139 --> 00:05:36.389
then the probability that they all
happen is the probability of all

85
00:05:36.389 --> 00:05:37.969
of them happening separately.

86
00:05:37.969 --> 00:05:39.322
So now let's look at some dice.

87
00:05:39.322 --> 00:05:45.728
Recall that when a dice is rolled,
a probability of obtaining a six is 1/6.

88
00:05:45.728 --> 00:05:50.727
So now when two dice are rolled,
what's the probability of obtaining 6,6?

89
00:05:50.727 --> 00:05:54.662
Well, we've calculated this before, but we
can actually do it with the product rule.

90
00:05:54.662 --> 00:06:01.371
This was 1/36 because we have 1 here and
36 cases.

91
00:06:01.371 --> 00:06:04.706
However, if we look at both
events separately, they're

92
00:06:04.706 --> 00:06:09.412
independent events because one rolling of
the dice does not affect the other one.

93
00:06:09.412 --> 00:06:13.647
And what's the probability that
the first one lands in six?

94
00:06:13.647 --> 00:06:15.446
Well, it's one sixth.

95
00:06:15.446 --> 00:06:18.678
And for
the second one it's again one sixth.

96
00:06:18.678 --> 00:06:23.314
So we multiply them and we get one

97
00:06:23.314 --> 00:06:28.650
sixth squared, which is 1/36.

98
00:06:28.650 --> 00:06:32.737
Now, what is the probability that
if I roll ten different dice,

99
00:06:32.737 --> 00:06:35.016
all of them fare, I get 10 sixes?

100
00:06:35.016 --> 00:06:39.223
Well, as you can imagine, the probability
is the probability of getting one sixth

101
00:06:39.223 --> 00:06:42.469
to the power of 10,
because all these roles are independent,

102
00:06:42.469 --> 00:06:46.098
that's one sixth to 10, which is a very,
very, very small number.

103
00:06:46.098 --> 00:06:48.240
So as you've learned in this video,

104
00:06:48.240 --> 00:06:51.971
the probability rule says that
if you have independent events,

105
00:06:51.971 --> 00:06:56.686
the calculation of the probability of all
of them happen at the same time is easy.

106
00:06:56.686 --> 00:06:58.060
It's just a product of all of them.