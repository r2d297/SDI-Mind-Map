WEBVTT

1
00:00:01.430 --> 00:00:05.250
Welcome to Week 1. This
week has two lessons.

2
00:00:05.250 --> 00:00:06.810
In the first lesson,
you will learn how to

3
00:00:06.810 --> 00:00:08.760
calculate probability
for different types

4
00:00:08.760 --> 00:00:10.350
of random events using

5
00:00:10.350 --> 00:00:12.645
rules of probability
and Bayes' theorem.

6
00:00:12.645 --> 00:00:15.390
In Lesson 2, I will introduce
you to the concept of

7
00:00:15.390 --> 00:00:17.160
a probability distribution and

8
00:00:17.160 --> 00:00:20.400
some examples of commonly used
probability distributions.

9
00:00:20.400 --> 00:00:22.320
But what exactly
is a probability?

10
00:00:22.320 --> 00:00:24.840
This is what we're going to
be looking at in this video.

11
00:00:24.840 --> 00:00:27.120
Simply put, probability is

12
00:00:27.120 --> 00:00:29.625
a measure of how likely
an event is to occur.

13
00:00:29.625 --> 00:00:32.295
For example, if I
throw a fair coin,

14
00:00:32.295 --> 00:00:34.110
the probability that it lands in

15
00:00:34.110 --> 00:00:36.790
heads is 50 percent or 1/2.

16
00:00:36.790 --> 00:00:38.400
If I throw a dice,

17
00:00:38.400 --> 00:00:42.285
the probability of it landing
in the number 4, is 1/6.

18
00:00:42.285 --> 00:00:45.180
Want to know more?
Let's get started.

19
00:00:45.180 --> 00:00:47.165
To get started, we're
going to explore

20
00:00:47.165 --> 00:00:48.530
an intriguing problem that will

21
00:00:48.530 --> 00:00:50.135
test your probability skills.

22
00:00:50.135 --> 00:00:52.670
Imagine you're in a
school with 10 kids and

23
00:00:52.670 --> 00:00:55.280
you want to randomly pick
a kid from the population.

24
00:00:55.280 --> 00:00:58.850
In this school, three kids
play soccer and seven don't.

25
00:00:58.850 --> 00:01:01.400
The question is, what is the
probability that the kid

26
00:01:01.400 --> 00:01:04.285
you picked at random
plays soccer?

27
00:01:04.285 --> 00:01:06.085
Are you ready to
find out the answer?

28
00:01:06.085 --> 00:01:07.790
Let's dive into the
world of probability and

29
00:01:07.790 --> 00:01:09.830
learn how to solve
this problem together.

30
00:01:09.830 --> 00:01:12.470
Recall that you want to find

31
00:01:12.470 --> 00:01:13.865
the probability
that a child picked

32
00:01:13.865 --> 00:01:15.890
at random plays soccer.

33
00:01:15.890 --> 00:01:18.620
In math, we have a way to
denote this statement.

34
00:01:18.620 --> 00:01:21.080
We will use P(soccer) to

35
00:01:21.080 --> 00:01:24.460
denote the probability
that the kid plays soccer.

36
00:01:24.460 --> 00:01:27.110
To find the probability
that a child plays

37
00:01:27.110 --> 00:01:29.720
soccer denoted by
P(soccer), first,

38
00:01:29.720 --> 00:01:32.030
we need to know the number
of kids who play soccer and

39
00:01:32.030 --> 00:01:34.855
the total number of
children in the school.

40
00:01:34.855 --> 00:01:37.595
We will express this in
the probability formula;

41
00:01:37.595 --> 00:01:40.205
number of kids who plays soccer

42
00:01:40.205 --> 00:01:43.645
divided by the total
number of kids.

43
00:01:43.645 --> 00:01:46.490
The probability of a
random kid playing soccer

44
00:01:46.490 --> 00:01:49.955
is 3/10 or 30 percent,

45
00:01:49.955 --> 00:01:53.125
can be also written as 0.3.

46
00:01:53.125 --> 00:01:56.390
The numerator is
represented by the event,

47
00:01:56.390 --> 00:01:58.565
the outcome's favorable
to the experiment,

48
00:01:58.565 --> 00:02:01.475
which in this case is the
kids who play soccer.

49
00:02:01.475 --> 00:02:04.030
The number of kids who
play soccer is three.

50
00:02:04.030 --> 00:02:05.925
That's the size of the event.

51
00:02:05.925 --> 00:02:08.690
The denominator corresponds
to the sample space,

52
00:02:08.690 --> 00:02:10.925
the total possible outcomes,

53
00:02:10.925 --> 00:02:13.850
and the number of those is 10.

54
00:02:13.850 --> 00:02:15.305
That's the size of

55
00:02:15.305 --> 00:02:17.815
the sample space, and
there you have it.

56
00:02:17.815 --> 00:02:19.580
We successfully
solved the problem

57
00:02:19.580 --> 00:02:21.605
using the basic principles
of probability.

58
00:02:21.605 --> 00:02:23.330
By understanding
this simple problem,

59
00:02:23.330 --> 00:02:25.130
you will be able to
apply these concepts in

60
00:02:25.130 --> 00:02:27.020
more complex
real-world situations

61
00:02:27.020 --> 00:02:29.015
in machine learning
and data science.

62
00:02:29.015 --> 00:02:31.150
Now, using the concept
of Venn diagrams,

63
00:02:31.150 --> 00:02:32.830
the total population,

64
00:02:32.830 --> 00:02:34.720
all the children are represented

65
00:02:34.720 --> 00:02:36.700
here by the green rectangle.

66
00:02:36.700 --> 00:02:39.445
This will be 100 percent
of the population.

67
00:02:39.445 --> 00:02:40.990
The green rectangle, including

68
00:02:40.990 --> 00:02:42.520
the kids who play
soccer and those who

69
00:02:42.520 --> 00:02:45.800
don't is the sample space,

70
00:02:45.800 --> 00:02:47.350
30 percent of the kids who play

71
00:02:47.350 --> 00:02:49.090
soccer will be in this circle.

72
00:02:49.090 --> 00:02:50.500
This is the event,

73
00:02:50.500 --> 00:02:53.270
the group of items
you're interested in.

74
00:02:53.270 --> 00:02:55.120
The kids who do not play soccer

75
00:02:55.120 --> 00:02:56.710
would be outside the circle,

76
00:02:56.710 --> 00:02:58.060
but still in the green rectangle

77
00:02:58.060 --> 00:02:59.770
because they're still
part of the population.

78
00:02:59.770 --> 00:03:01.495
We can calculate the probability

79
00:03:01.495 --> 00:03:02.950
by dividing the number of

80
00:03:02.950 --> 00:03:04.060
favorable outcomes by

81
00:03:04.060 --> 00:03:06.130
the total number of
possible outcomes.

82
00:03:06.130 --> 00:03:08.080
In our next example, we're
going to be flipping a coin.

83
00:03:08.080 --> 00:03:09.190
When we do that,

84
00:03:09.190 --> 00:03:11.520
the coin can land
in heads or tails.

85
00:03:11.520 --> 00:03:13.220
Because this activity
of flipping a coin

86
00:03:13.220 --> 00:03:15.590
producing an outcome
that is uncertain,

87
00:03:15.590 --> 00:03:17.705
we're going to call
this the experiment.

88
00:03:17.705 --> 00:03:20.450
In probability, an experiment
is any process that

89
00:03:20.450 --> 00:03:23.240
produces an outcome
that is uncertain.

90
00:03:23.240 --> 00:03:24.905
Thus, in our content,

91
00:03:24.905 --> 00:03:26.715
throwing a coin
is an experiment.

92
00:03:26.715 --> 00:03:29.780
We'll determine the probability
of the coin landing in

93
00:03:29.780 --> 00:03:33.535
heads denoted by P(heads).

94
00:03:33.535 --> 00:03:35.865
We're going to be flipping
a fair coin meaning that

95
00:03:35.865 --> 00:03:40.445
each outcome heads or tails
is equally likely to occur.

96
00:03:40.445 --> 00:03:43.345
Both of them occur with
50 percent probability.

97
00:03:43.345 --> 00:03:46.280
P(heads) is equal
to the event of

98
00:03:46.280 --> 00:03:50.045
landing in heads divided by
the total number of outcomes,

99
00:03:50.045 --> 00:03:53.950
and that's 1/2 or 0.5.

100
00:03:53.950 --> 00:03:55.550
Now let's make the
problem a bit more

101
00:03:55.550 --> 00:03:57.350
complex and throw two coins.

102
00:03:57.350 --> 00:03:58.790
What will be the probability

103
00:03:58.790 --> 00:04:00.740
of both of them landing heads?

104
00:04:00.740 --> 00:04:02.570
To answer this question,
let's work through

105
00:04:02.570 --> 00:04:05.660
the experiment to determine
the total number of outcomes.

106
00:04:05.660 --> 00:04:08.605
The first coin can land
in heads or tails.

107
00:04:08.605 --> 00:04:11.310
Now for each outcome
of the first coin,

108
00:04:11.310 --> 00:04:14.430
the second one can land
in heads or tails.

109
00:04:14.430 --> 00:04:17.850
Our final outcomes
are, heads heads,

110
00:04:17.850 --> 00:04:24.090
heads tails, tails
heads, and tails tails.

111
00:04:24.090 --> 00:04:26.685
Those are four outcomes.

112
00:04:26.685 --> 00:04:28.310
Now, with these outcomes,

113
00:04:28.310 --> 00:04:32.195
what is the probability of
both coins landing in heads?

114
00:04:32.195 --> 00:04:34.480
That is the upcoming quiz.

115
00:04:34.480 --> 00:04:36.200
Out of these four
possible outcomes,

116
00:04:36.200 --> 00:04:37.610
we're interested
in the one where

117
00:04:37.610 --> 00:04:39.395
both coins land in heads.

118
00:04:39.395 --> 00:04:43.630
There's only one such outcome
which is heads heads.

119
00:04:43.630 --> 00:04:46.140
The probability of both
coins landing in heads,

120
00:04:46.140 --> 00:04:50.990
denoted as P(HH) is the
number of favorable outcomes,

121
00:04:50.990 --> 00:04:52.160
which is one,

122
00:04:52.160 --> 00:04:55.070
divided by the total number
of outcomes, which is four,

123
00:04:55.070 --> 00:04:58.965
so that's 1/4 or 0.25,

124
00:04:58.965 --> 00:05:00.900
also called 25 percent.

125
00:05:00.900 --> 00:05:04.545
That's the probability of
both coins landing in heads.

126
00:05:04.545 --> 00:05:06.690
Now, what if we
flipped three coins?

127
00:05:06.690 --> 00:05:08.885
Well, let's calculate
the probability of

128
00:05:08.885 --> 00:05:10.100
the three of them landing in

129
00:05:10.100 --> 00:05:11.920
heads when you
throw three coins.

130
00:05:11.920 --> 00:05:13.790
We can throw the
first coin and it

131
00:05:13.790 --> 00:05:15.470
can land in heads or tails.

132
00:05:15.470 --> 00:05:17.630
Now, the second coin
for each outcome of

133
00:05:17.630 --> 00:05:20.380
the first coin can land
in heads or tails.

134
00:05:20.380 --> 00:05:23.165
The third coin, for
each outcome of

135
00:05:23.165 --> 00:05:27.080
the first and second coins
can land in heads or tails.

136
00:05:27.080 --> 00:05:30.695
How many total outcomes we
have? We have eight of them.

137
00:05:30.695 --> 00:05:36.555
All heads, heads heads
tails, heads tails heads,

138
00:05:36.555 --> 00:05:40.215
heads tails tails,
tails heads heads,

139
00:05:40.215 --> 00:05:42.090
tails heads tails,

140
00:05:42.090 --> 00:05:43.800
tails tails heads,

141
00:05:43.800 --> 00:05:45.915
and tails tails tails.

142
00:05:45.915 --> 00:05:47.570
That is eight outcomes.

143
00:05:47.570 --> 00:05:49.070
Now the question for you is,

144
00:05:49.070 --> 00:05:53.590
what's the probability of
landing on heads three times?

145
00:05:53.590 --> 00:05:55.730
Well, out of these eight
possible outcomes,

146
00:05:55.730 --> 00:05:57.245
we're interested
in the one where

147
00:05:57.245 --> 00:05:59.135
the three of them land in heads.

148
00:05:59.135 --> 00:06:01.160
That is one divided by

149
00:06:01.160 --> 00:06:03.410
the total number of
outcomes, which is eight.

150
00:06:03.410 --> 00:06:07.560
Therefore the answer
is 1/8 or 0.125.