---
layout: page
title: Twitter Sentiment Analysis
description: 
img: assets/img/12.jpg
importance: 1
category: work
related_publications: false
---

### Summary:

- Accessed Twitter’s API to download tweets.
- Derived the sentiments (attitudes or perceptions) of tweets using Finn Arup Nielsen’s list of words rated for valence in python.
- Computed the sentiment of new terms that did NOT exist in Finn Arup Nielsen’s list of words rated for valence by computing the average sentiment scores of the tweets that contained the new words.
- Analyzed the relationship between location and mood from tweet sentiments.

#### Files:

- output_copy_3.txt:
  - The processed Twitter data downloaded from the live Twitter stream using the development API.
- tweet_sentiment.py:
  - A script that computes the sentiment of each tweet based on the sentiment scores of the terms in the tweet. The sentiment of a tweet is equivalent to the sum of the sentiment scores for each term in the tweet. Each word or phrase that is found in a tweet but not found in AFINN-111.txt is given a sentiment score of 0.
- AFINN-111.txt:
  - A list of pre-computed sentiment scores. Each line in the file contains a word or phrase followed by a sentiment score. This file is used to compute the tweet sentiments in tweet_sentiment.py.
- term_sentiment.py:
  - A script that computes the sentiment for the terms that do not appear in the file AFINN-111.txt.
- term_sentiment_output.txt:
  - The output of term_sentiment.py. This is needed to run the happiest_state.py file.
- frequency.py:
  - A script that computes the term frequency histogram of the livestream data harvested. The frequency of a term is calculated as [# of occurrences of the term in all tweets]/[# of occurrences of all terms in all tweets].
- happiest_state.py:
  - A script that computes the happiest state. The script returns the two-letter state abbreviation of the state with the highest average tweet sentiment.
- top_ten.py:
  - A script that computes the ten most frequently occurring hashtags in the downloaded tweets.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
