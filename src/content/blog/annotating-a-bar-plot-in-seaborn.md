---
title: "Annotating a bar plot in seaborn"
description: "Read this short port if you are searching for a quick solution to annotate a barplot in seaborn"
pubDate: "Jun 01 2023"
heroImage: "/seaborn-bar-plot-hero-image.png"
heroImageAlt: "A seaborn bar plot with four bars"
---

Seaborn is a python library built on top of Matplotlib and it provides a high-level interface for creating stunning and informative statistical graphics. In this blog post, I won’t dive into the world of Seaborn - instead of exploring its key features, advantages, and how it can help you unlock powerful insights from your data, I just want to show you a quick solution for <b>annotating a bar plot in seaborn with just one line of code</b>.

If you are interested in the data that I analyzed as well as in the code I used please look into this notebook.
Otherwise just enjoy the code snippet.

```py
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_theme(style="whitegrid")
ax = sns.countplot(x='sales_method',
              data=df_clean,
              order=['Email', 'Call', 'Email + Call'],
              palette=['#003f5c', '#58508d', '#bc5090'])

ax.set_title('Most of the customers received emails only',
    fontsize=10)
ax.set_xlabel('Sales Method')
ax.set_ylabel('Count of Customers')
ax = plt.suptitle('Count of customers for each approach')
    
plt.show()
```
---
This code produces the following plot. As you can see the blue bar is slightly below 7.000 but we do not know the exact number. This is bad if you need to show this information to your audience.

<img src="/seaborn-bar-plot-without-annotation.png" alt="seaborn-bar-plot-without-annotation">

Only the following line of code is missing in the code block above to show the annotation above each bar.

```py
ax.bar_label(ax.containers[0], fontsize=10)
```
---
I added this line of code after assigning the sns.counplot-function to ax and before setting the title. 

```py
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_theme(style="whitegrid")
ax = sns.countplot(x='sales_method',
              data=df_clean,
              order=['Email', 'Call', 'Email + Call'],
              palette=['#003f5c', '#58508d', '#bc5090'])

ax.bar_label(ax.containers[0], fontsize=10)

ax.set_title('Most of the customers received emails only',
    fontsize=10)
ax.set_xlabel('Sales Method')
ax.set_ylabel('Count of Customers')
ax = plt.suptitle('Count of customers for each approach')
    
plt.show()
```
---
If we look at the plot now, we have all necessary information and can see that the blue bar shows a value of 6.921.

<img src="/seaborn-bar-plot-with-annotation.png" alt="/seaborn-bar-plot-with-annotation">

I hope this can help you.