---
layout:     post
title:      Recommendation System for News DAY1
subtitle:   Question Understanding and Baseline
date:       2020-11-25
author:     Shuo Wang
header-img:  img/post-bg-swift2.jpg
catalog: true
tags:
    - recommendation system
    - news
    - recall
    - CF
---

# The problem description
News recommended scenario, this match the user behavior prediction of challenge, the problem is the news in the news APP is recommended as the background, purpose is to ** asked us news articles according to user's browsing history click data information to predict users click on the behavior of the future, namely the user's last click the news article ** , this problem is designed to guide you to understand some of the recommendation system's business background, solving practical problems.

# Data description
There are 300,000 users, nearly 3 million clicks, a total of 360,000 different news articles, and each news article has corresponding embedding vector presentation. The click log data of 200,000 users is selected as the training set, the click log data of 50,000 users as the test set A, and the click log data of 50,000 users as the test set B.

# The formula of evaluation index
$$
score(user) = \sum_{k=1}^5 \frac{s(user, k)}{k}
$$

for example, s(user1,1) =1 as the rest of s(user1,2), s(user1,3), s(user1, 4), s(user1, 5) is 0. So the higher rank will have a higher value. If there is no article targeted, score(user1) = 0.

# Key points
- only predict the last article news
- convert log info to: features + labels(click on the probability, then, it is a classification question)

```python
# import packages
import time, math, os
from tqdm import tqdm
import gc
import pickle
import random
from datetime import datetime
from operator import itemgetter
import numpy as np
import pandas as pd
import warnings
from collections import defaultdict
warnings.filterwarnings('ignore')

```


```python
data_path = './data_raw/'
save_path = './tmp_results/'
```

To be continue...
