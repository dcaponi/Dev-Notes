# Naive Bayes

#### Bayes Theorem

$$
P(A|B) = \frac {P(B|A) * P(A)} {P(B)}
$$

The probability of event A given condition B occurs is:

* Past occurrences of event A when B condition was present `P(B|A)` as a percentage of all observations
* Times event A happened out of all observations `P(A)`
* Times condition B was present out of all observations `P(B)`

#### Key Assumption - All features of an observation are independent of each other

Saying this key thing means we now can represent `P(B|A)` as:

$P(B|A) = P(b_1 | A) * P(b_2 | A) *P(b_3 | A) ... P(b_n |A) = \Pi_{i=1}^nP(b_i | A) $

and `P(B)` is now:

$P(B) = P(b_1)*P(b_2)*P(b_3) ... P(b_n) = \Pi_{i=1}^n P(b_i)$

where n is the number of features in an observation

$\Pi_{i=1}^nP(b_i)$ becomes a constnat and drops so now the equation is:
$$
Maximum (P(A|B) = P(A) \times \Pi_{i=1}^nP(b_i | A))
$$

 #### Example

| i    | weather | temp | humidity | wind | Golf? |
| ---- | :------ | ---- | -------- | ---- | ----- |
| 1    | Rain    | Hot  | Hum      | No   | No    |
| 2    | Rain    | Hot  | Hum      | Yes  | No    |
| 3    | Cloud   | Hot  | Hum      | No   | Yes   |
| 4    | Sun     | Mild | Hum      | No   | Yes   |
| 5    | Sun     | Cold | Not      | No   | Yes   |
| 6    | Sun     | Cold | Not      | Yes  | No    |
| 7    | Cloud   | Cold | Not      | Yes  | Yes   |
| 8    | Rain    | Mild | Hum      | No   | No    |
| 9    | Rain    | Cold | Not      | No   | Yes   |
| 10   | Sun     | Mild | Not      | No   | Yes   |
| 11   | Rain    | Mild | Not      | Yes  | Yes   |
| 12   | Cloud   | Mild | Hum      | Yes  | Yes   |
| 13   | Cloud   | Hot  | Not      | No   | Yes   |
| 14   | Sun     | Mild | Hum      | Yes  | Yes   |

Consider the table of whether or not one went golfing. 

* There are 4 features: weather, temp, humid, wind
* The target is "Golf?"
* There are 9 total yesses and 5 total nos for a total of 14 observations

Step 1:  Compute $P(b_i | A)$ for all four features

Weather

|       | Yes  | No   | P(Yes) = Yes for feature value / All yesses | P(Yes) = No for feature value / All nos |
| ----- | ---- | ---- | ------------------------------------------- | --------------------------------------- |
| Sun   | 2    | 3    | 2/9                                         | 3/5                                     |
| Rain  | 4    | 0    | 4/9                                         | 0/5                                     |
| Cloud | 3    | 2    | 3/9                                         | 2/5                                     |

Temp

|      | Yes  | No   | P(Yes) = Yes for feature value / All yesses | P(Yes) = No for feature value / All nos |
| ---- | ---- | ---- | ------------------------------------------- | --------------------------------------- |
| Hot  | 2    | 2    | 2/9                                         | 2/5                                     |
| Mild | 4    | 2    | 4/9                                         | 2/5                                     |
| Cold | 3    | 1    | 3/9                                         | 1/5                                     |

Humidity

|      | Yes  | No   | P(Yes) = Yes for feature value / All yesses | P(Yes) = No for feature value / All nos |
| ---- | ---- | ---- | ------------------------------------------- | --------------------------------------- |
| High | 3    | 4    | 3/9                                         | 4/5                                     |
| None | 6    | 1    | 6/9                                         | 1/5                                     |

Wind

|      | Yes  | No   | P(Yes) = Yes for feature value / All yesses | P(Yes) = No for feature value / All nos |
| ---- | ---- | ---- | ------------------------------------------- | --------------------------------------- |
| High | 3    | 3    | 3/9                                         | 3/5                                     |
| None | 6    | 2    | 6/9                                         | 2/5                                     |

Step 2: Given the conditions sunny, hot, no humidity and no wind, select the relevant rows from our tables above

Sunny:  yes 2/9  no 3/5 

​	_2 of the 9 total times we said yes, and 3 of the 5 times we said no it was sunny_

Hot: yes 2/9  no 2/5

​	_2 of the 9 total times we said yes, and 2 of the 5 times we said no it was hot_

Not Humid: yes 6/9 no 1/5

​	_6 of the 9 total times we said yes, and 1 of the 5 times we said no it was not humid_

Not Windy: yes 6/9 no 2/5

​	_6 of the 9 total times we said yes, and 2 of the 5 times we said no it was not windy_

Step 3: Multiply all the yes fractions by the total fraction of yesses out of all observations (9 yesses / 14 observations)

$P(Yes | Conditions) = 2/9 * 2/9 * 6/9 * 6/9 * 9/14 = 0.014$

Step 3b: Repeat for the other possible outcome, the nos

$P(No | Conditions) = 3/5 * 2/5 * 1/5 * 2/5 * 5/14 = 0.0068$

Step 4: take the higher value - 0.014

Thus given the conditions, we're **More likely to go golfing given these conditions than not**



