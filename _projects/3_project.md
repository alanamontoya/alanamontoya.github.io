---
layout: page
title: A Comparative Analysis of De-Identification Tools on Health Data 
description: 
img: assets/img/slide_1.jpg
importance: 3
---

So, my paper was “A Comparative Analysis of Speed and Accuracy for Three Off-the-Shelf De-Identification Tools.” Basically, it starts off by providing the motivation. So, there is a lot of health data being stored in Electronic Health Records which also contains a free-text section about patients and their treatments. This free text data could be very useful for research, though due to the nature of this data it contains a lot of sensitive information, or PII. The challenge is then how to share this data with the research community without compromising patient confidentiality and privacy rights.
There has been a lot of work done to automate the process of removing PII, but there is a lack of comparing the performance between these various approaches. So, this paper takes three off-the-shelf de-identification systems and uses publicly available corpora to assess each of the system’s speed and accuracy in a controlled comparative analysis. 

{% include figure.liquid loading="eager" path="assets/img/slide_1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}

Slide 2:
The process first started by identifying which annotations to assess each of the system’s accuracy from. They considered HIPAA’s Privacy Rule “Safe Harbor” method which consists of eighteen categories of PII that the de-identification system would need to target. But, since the three systems do not address all of these, the categories were narrowed down to two sets: shared categories which are those that all three systems target and specialty categories which only two of the systems target. Accuracy was determined for both individual PII categories as well as PII as a whole, that is, a system could wrongly identify the PII category but would still count as true positive for identifying that it was PII.
Next, they determined the reference corpora to use which were the 2014 and 2016 i2b2 de-identification challenge corpora, both of which were publicly available. The 2014 corpus was split into 790 training notes and 514 test notes, and the 2016 corpus was split into 200 development notes, 600 training notes, and 400 test notes. The notes in the 2016 corpus tended to be longer with an average of 1,863 words per note versus 617 words per note in the 2014 corpus.
Both corpora were processed as plain text files with one note per file and all three of the de-identification systems were tested out-of-the-box.

Slide 3:
The paper then discusses the three text de-identification systems that would be evaluated. The first is Amazon Comprehend Medical which is a cloud-based natural language processing system. For this system, they focused on the detect phi service endpoint, which can be run using API calls or remotely on an AWS instance. To test the system, they used a simple Python script to read in a note, post it to the service endpoint, and then convert the returned output to the brat standoff format.
The next system was Clinacuity’s CliniDeID. The on-premises version can use a graphical user-interface or the command-line, though in the paper they used the command line. This system offers multiple levels of de-identification, so they chose the ‘Beyond HIPAA Safe Harbor’ level because it better aligned with the categories of the other systems. Testing was done using a special testing license.
The third system was the National Library of Medicine’s Scrubber. This system is also on-premises and can be used through either a graphical user-interface or the command-line. This system outputs a redacted version of the original note. However, since the other systems output annotated offsets or the reference corpus, they needed to write a script to map the NLM Scrubber’s output file to the annotation format by lining up the preceding and following context around all bracketed redacted forms.
To generate accuracy metrics for the systems, they used ETUDE (Evaluation Tool for Unstructured Data and Extractions). This tool evaluates each of the reference and system documents based on corpus specific configuration files. They also used a partial matching flag to evaluate annotations, meaning that as long as two annotations matched categories and their spans at least partially overlapped it would be considered a true positive.

Slide 4:
Next, I can talk about the results. So, the National Library of Medicine’s Scrubber was by far the fastest. It was about twice as fast at processing ten thousand characters as compared to Amazon Comprehend and about 14 times faster than CliniDeID. The NLM Scrubber was also much better at processing more characters per second as compared to the two other systems. But the NLM Scrubber failed to process four notes which was due to non-ASCII characters being present. Amazon Comprehend also did not process thirty-five notes, which ended up being the thirty-five longest notes, so this could be an opportunity for this system to improve its timing.

Slide 5:
As for accuracy, we can see that CliniDeID performed substantially better than the other two systems. Amazon Comprehend tended to perform better than the NLM Scrubber except for the address category, though overall Amazon Comprehend and the NLM Scrubber tended to perform relatively similarly. CliniDeID had challenges with the eAddress and ID categories and the NLM Scrubber had difficulties with the age category.
