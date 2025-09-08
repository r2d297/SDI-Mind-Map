WEBVTT

1
00:00:00.000 --> 00:00:02.320
Welcome back. You've
seen a lot of

2
00:00:02.320 --> 00:00:04.550
fascinating concepts
of probability so far.

3
00:00:04.550 --> 00:00:06.370
In this lesson, we
will take a look

4
00:00:06.370 --> 00:00:08.585
at the concept of
conditional probability.

5
00:00:08.585 --> 00:00:10.210
Conditional probability is all

6
00:00:10.210 --> 00:00:11.650
about calculating
the probability of

7
00:00:11.650 --> 00:00:13.360
an event happening given

8
00:00:13.360 --> 00:00:15.550
that another event
has already happened.

9
00:00:15.550 --> 00:00:18.220
For example, let's say you are

10
00:00:18.220 --> 00:00:21.370
wondering about the probability
that today is humid,

11
00:00:21.370 --> 00:00:23.155
that is some number.

12
00:00:23.155 --> 00:00:27.025
However, if you found out
that yesterday was raining,

13
00:00:27.025 --> 00:00:29.440
the probability that
today is humid changes,

14
00:00:29.440 --> 00:00:32.045
that is a conditional
probability.

15
00:00:32.045 --> 00:00:34.450
In a previous lesson, we
established the probability of

16
00:00:34.450 --> 00:00:37.110
obtaining two heads when you
throw two coins as follows.

17
00:00:37.110 --> 00:00:38.695
Let me recap very quickly.

18
00:00:38.695 --> 00:00:40.330
The first head can
be heads or tails,

19
00:00:40.330 --> 00:00:42.480
and for each option
of these two,

20
00:00:42.480 --> 00:00:44.060
the second one can
be heads or tails,

21
00:00:44.060 --> 00:00:46.070
so we have four
possibilities: Head heads,

22
00:00:46.070 --> 00:00:48.750
head tails, tail heads
and tails tails.

23
00:00:48.750 --> 00:00:50.915
The probability of
heads heads, well,

24
00:00:50.915 --> 00:00:52.865
the sample space was of size 4

25
00:00:52.865 --> 00:00:55.370
and the event was of size 1,

26
00:00:55.370 --> 00:00:57.500
so it was 1/4.

27
00:00:57.500 --> 00:00:59.440
Now let me ask you a question.

28
00:00:59.440 --> 00:01:02.780
What is the probability
that both coins land on

29
00:01:02.780 --> 00:01:07.055
heads if you know that the
first one landed in heads?

30
00:01:07.055 --> 00:01:08.285
Now you have more information.

31
00:01:08.285 --> 00:01:11.450
I came and told you that the
first coin landed in heads.

32
00:01:11.450 --> 00:01:13.160
Now, what is the probability

33
00:01:13.160 --> 00:01:15.160
that both of them
landed in heads?

34
00:01:15.160 --> 00:01:17.650
Well, if the first
one landed in heads,

35
00:01:17.650 --> 00:01:19.040
then we live here.

36
00:01:19.040 --> 00:01:20.630
This is a new sample space.

37
00:01:20.630 --> 00:01:22.520
The bottom part
doesn't count anymore

38
00:01:22.520 --> 00:01:26.440
because the first coin landed
in heads and not tails.

39
00:01:26.440 --> 00:01:31.100
Now the denominator is
not four, but it's two,

40
00:01:31.100 --> 00:01:33.080
because now there's
two cases instead of

41
00:01:33.080 --> 00:01:35.540
four and we still have
one favorable outcome,

42
00:01:35.540 --> 00:01:38.365
so the new answer is 1/2.

43
00:01:38.365 --> 00:01:40.520
This over here is called

44
00:01:40.520 --> 00:01:42.590
a conditional probability and we

45
00:01:42.590 --> 00:01:44.780
denote it with a vertical bar.

46
00:01:44.780 --> 00:01:46.415
The probability of heads heads,

47
00:01:46.415 --> 00:01:48.890
given that the first is heads.

48
00:01:48.890 --> 00:01:52.385
That given that is denoted
by a vertical bar,

49
00:01:52.385 --> 00:01:54.680
and this is a
conditional probability.

50
00:01:54.680 --> 00:01:57.550
This can be seen in
a table as follows.

51
00:01:57.550 --> 00:01:58.640
If the first coin is on

52
00:01:58.640 --> 00:02:00.680
the left and the
second coin is on top,

53
00:02:00.680 --> 00:02:03.470
then these are the
four possibilities.

54
00:02:03.470 --> 00:02:04.520
Heads heads, heads tails,

55
00:02:04.520 --> 00:02:06.415
tails heads and tails tails.

56
00:02:06.415 --> 00:02:07.790
We're going to look
at the probability

57
00:02:07.790 --> 00:02:08.885
of landing our heads twice,

58
00:02:08.885 --> 00:02:11.195
given that the
first one is heads.

59
00:02:11.195 --> 00:02:13.480
We live in this first row.

60
00:02:13.480 --> 00:02:15.200
When we live in the first row,

61
00:02:15.200 --> 00:02:19.910
our sample space now has size
2 and our event has size 1.

62
00:02:19.910 --> 00:02:21.560
Therefore, the probability is

63
00:02:21.560 --> 00:02:24.450
not 1/4 anymore, is now 1/2.

64
00:02:24.460 --> 00:02:27.920
Now, let me ask you
another question.

65
00:02:27.920 --> 00:02:30.395
What is the probability
of landing in heads twice

66
00:02:30.395 --> 00:02:34.340
given that the first
coin landed in tails?

67
00:02:34.340 --> 00:02:36.895
Slightly different
question, give it a try.

68
00:02:36.895 --> 00:02:39.000
Well, if the first coin

69
00:02:39.000 --> 00:02:40.475
landed in tails, now
we're live here.

70
00:02:40.475 --> 00:02:42.425
This is our sample
space and the top

71
00:02:42.425 --> 00:02:44.550
is not valid anymore.

72
00:02:44.550 --> 00:02:48.080
The denominator is now two,

73
00:02:48.080 --> 00:02:49.490
but the numerator is zero

74
00:02:49.490 --> 00:02:51.320
because now there's
no heads heads,

75
00:02:51.320 --> 00:02:55.720
so the answer is
0/2, which is zero.

76
00:02:55.720 --> 00:02:57.420
This makes sense, because

77
00:02:57.420 --> 00:02:58.580
if one of them landed in tails,

78
00:02:58.580 --> 00:03:02.615
there's no way that they're
both going to land in heads.

79
00:03:02.615 --> 00:03:04.970
This condition really
changed the probability

80
00:03:04.970 --> 00:03:07.660
from 1/4 all the way to zero.

81
00:03:07.660 --> 00:03:11.660
Again, we can see it as
a table where we have

82
00:03:11.660 --> 00:03:14.805
the four cases and

83
00:03:14.805 --> 00:03:16.250
we want to calculate
the probability

84
00:03:16.250 --> 00:03:17.615
of landing in heads twice,

85
00:03:17.615 --> 00:03:19.220
given that the
first one is tails,

86
00:03:19.220 --> 00:03:23.100
means we live in the second
row, not in the first one.

87
00:03:24.310 --> 00:03:28.810
Well in the bottom we have
a sample space of size 2,

88
00:03:28.810 --> 00:03:30.170
but on the top we have

89
00:03:30.170 --> 00:03:32.230
nothing because
there's no heads heads

90
00:03:32.230 --> 00:03:36.260
in the sample space and
therefore the number is zero.

91
00:03:36.260 --> 00:03:38.695
As you can see, condition

92
00:03:38.695 --> 00:03:41.030
can change the
probability of an event,

93
00:03:41.030 --> 00:03:43.705
and this is what we study
with conditional probability.

94
00:03:43.705 --> 00:03:46.840
Let's recall the product
rule for independent events.

95
00:03:46.840 --> 00:03:47.940
It said that the probability of

96
00:03:47.940 --> 00:03:51.005
A intersection B is P(A) *P(B).

97
00:03:51.005 --> 00:03:54.945
But this only happen when
A and B were independent.

98
00:03:54.945 --> 00:03:56.580
That doesn't always happen.

99
00:03:56.580 --> 00:03:59.390
Let me give you an example
of something where

100
00:03:59.390 --> 00:04:00.950
the events are not

101
00:04:00.950 --> 00:04:03.435
independent. Let me
ask you a question.

102
00:04:03.435 --> 00:04:06.500
What is the probability
if I roll two dice that

103
00:04:06.500 --> 00:04:11.265
the first one lands on six
and that the sum is 10.

104
00:04:11.265 --> 00:04:13.195
Well, we have a space of

105
00:04:13.195 --> 00:04:18.460
36 possibilities because
it's pairs of numbers.

106
00:04:18.460 --> 00:04:20.885
The only favorable one is 6, 4,

107
00:04:20.885 --> 00:04:23.680
because if the first one
is six and the sum is 10,

108
00:04:23.680 --> 00:04:25.250
the second one has to be four.

109
00:04:25.250 --> 00:04:31.830
The probability is 1/36
total ones and that's 1/36.

110
00:04:31.830 --> 00:04:34.760
Now, let's look at in a
slightly different way.

111
00:04:34.760 --> 00:04:37.880
Let's try to apply
the product rule.

112
00:04:37.880 --> 00:04:39.790
We want the probability
that the first one is

113
00:04:39.790 --> 00:04:41.680
six and that the sum is 10.

114
00:04:41.680 --> 00:04:43.390
We would like to

115
00:04:43.390 --> 00:04:46.055
have the probability that
the first one is six.

116
00:04:46.055 --> 00:04:49.375
Well, that is over here,

117
00:04:49.375 --> 00:04:54.490
so that is 6/36.

118
00:04:54.490 --> 00:04:57.320
Now what I have to
multiply this to obtain

119
00:04:57.320 --> 00:05:00.490
the probability that the first
is six and the sum is 10?

120
00:05:00.490 --> 00:05:05.000
Well, I need the probability
that the sum is 10,

121
00:05:05.000 --> 00:05:08.450
but among the ones for
which the first is six.

122
00:05:08.450 --> 00:05:10.565
That is this event over here,

123
00:05:10.565 --> 00:05:13.800
this 6,4 divided by the six,

124
00:05:13.800 --> 00:05:16.455
where the first one is six,

125
00:05:16.455 --> 00:05:18.915
and that is 1/36,

126
00:05:18.915 --> 00:05:21.400
which is what we obtained
here previously.

127
00:05:21.400 --> 00:05:24.290
To summarize, we have that

128
00:05:24.290 --> 00:05:26.360
the probability of
A intersection B,

129
00:05:26.360 --> 00:05:28.820
notice that the first is
six and that the sum is 10,

130
00:05:28.820 --> 00:05:31.190
is the probability of the
first one that the first is

131
00:05:31.190 --> 00:05:33.620
six times the probability

132
00:05:33.620 --> 00:05:35.705
of the second one
given the first one.

133
00:05:35.705 --> 00:05:37.655
We need that given
the first one.

134
00:05:37.655 --> 00:05:39.140
Because we need to multiply

135
00:05:39.140 --> 00:05:40.505
by the probability
that the sum is 10,

136
00:05:40.505 --> 00:05:42.215
given that the first is six.

137
00:05:42.215 --> 00:05:44.870
We get a slightly
different formula.

138
00:05:44.870 --> 00:05:47.875
Probability of A intersection
B is the probability of

139
00:05:47.875 --> 00:05:51.470
A times the probability
of B given A.

140
00:05:51.470 --> 00:05:53.360
Now, when they're independent,

141
00:05:53.360 --> 00:05:54.860
then probability of B given A

142
00:05:54.860 --> 00:05:56.420
is the same as
probability of B because

143
00:05:56.420 --> 00:06:00.205
A doesn't make any difference
on the occurrence of B.

144
00:06:00.205 --> 00:06:02.090
When they're independent, it

145
00:06:02.090 --> 00:06:05.375
actually translates
to B(A)*P(B).

146
00:06:05.375 --> 00:06:09.530
But in the general
case, is P(A)*P(B|A).

147
00:06:09.530 --> 00:06:13.670
That is the general product
rule that works every time.

148
00:06:13.670 --> 00:06:15.200
That means when the events are

149
00:06:15.200 --> 00:06:17.890
independent and when
they're not independent.

150
00:06:17.890 --> 00:06:19.500
Now let's look at
the dice example.

151
00:06:19.500 --> 00:06:21.240
Here's a question that
you've seen before.

152
00:06:21.240 --> 00:06:23.480
What is the probability that
the sum of two dice that

153
00:06:23.480 --> 00:06:25.760
I throw randomly is 10?

154
00:06:25.760 --> 00:06:27.965
Well, there's three cases

155
00:06:27.965 --> 00:06:30.820
divided by the total 36 of them.

156
00:06:30.820 --> 00:06:33.140
The answer is 3/36,

157
00:06:33.140 --> 00:06:36.620
which in lowest
terms, it's 1/12.

158
00:06:36.620 --> 00:06:39.795
Now, let's put a condition.

159
00:06:39.795 --> 00:06:42.170
I'm telling you that I

160
00:06:42.170 --> 00:06:45.560
looked at the first one and
the first one is a six.

161
00:06:45.560 --> 00:06:48.485
What is the probability
that now the sum is 10,

162
00:06:48.485 --> 00:06:50.785
given that the first one is six?

163
00:06:50.785 --> 00:06:52.785
Well, let's calculate it.

164
00:06:52.785 --> 00:06:54.570
Because the first one is six,

165
00:06:54.570 --> 00:06:56.900
now we live on this bottom row.

166
00:06:56.900 --> 00:06:59.420
The top five rows don't
matter anymore because

167
00:06:59.420 --> 00:07:02.380
our new sample space is
just this bottom row.

168
00:07:02.380 --> 00:07:05.045
Among this bottom row, well,

169
00:07:05.045 --> 00:07:08.180
there's six cases and one
of them is favorable,

170
00:07:08.180 --> 00:07:11.105
so the probability is now 1/6.

171
00:07:11.105 --> 00:07:14.725
The probability change
from 1/12 to 1/6.

172
00:07:14.725 --> 00:07:17.010
Now let's look at
another problem.

173
00:07:17.010 --> 00:07:19.730
What is the probability
that the sum is 10.

174
00:07:19.730 --> 00:07:23.450
But now the condition is that
the first one was a one.

175
00:07:23.450 --> 00:07:24.780
I looked and the
first one was a one.

176
00:07:24.780 --> 00:07:28.555
Now, what is the probability
that the sum of them is 10?

177
00:07:28.555 --> 00:07:31.235
Well, if the first one is a one,

178
00:07:31.235 --> 00:07:34.210
then now we live on this row
over here, the first one.

179
00:07:34.210 --> 00:07:37.835
On this row, there's six
elements and none of them

180
00:07:37.835 --> 00:07:41.750
satisfy that the sum is 10,

181
00:07:41.750 --> 00:07:43.145
because the ones
where the sum is

182
00:07:43.145 --> 00:07:45.070
10 are on the very bottom.

183
00:07:45.070 --> 00:07:47.850
Therefore, the probability
is zero. It makes sense.

184
00:07:47.850 --> 00:07:49.500
If the first one is a one,

185
00:07:49.500 --> 00:07:51.110
there's no way I can
add a 10 because

186
00:07:51.110 --> 00:07:53.530
the second one can
at most be a six,

187
00:07:53.530 --> 00:07:56.970
so this probably
changed to zero.