---
layout: page
title: Healthcare PII Redaction
description: 
img: assets/img/slide_1.jpg
importance: 3
---

I presented an overview of the findings from a journal article titled “A Comparative Analysis of Speed and Accuracy for Three Off-the-Shelf De-Identification Tools” by Paul M. Heider, PhD, Jihad S. Obeid, MD, and Stéphane M. Meystre, MD, PhD. The detailed article can be found here: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7233098/.

There exists a significant amount of health data stored in Electronic Health Records which contain free-text sections about patients and their treatments. Although this free text data could be very useful for research purposes, the nature of this data contains sensitive patient information, or PII. The challenge is then how to share this data with the research community without compromising patient confidentiality and privacy rights.

While there has been efforts to automate the process of removing PII, there is a lack of comparing the performance between the various approaches. This paper took three off-the-shelf de-identification systems and used publicly available corpora to assess each of the system’s speed and accuracy in a controlled comparative analysis. The de-identification systems included Amazon Comprehend Medical PHId, Clinacuity’s CliniDeID, and the National Library of Medicine’s (NLM) Scrubber.

{% include figure.liquid loading="eager" path="assets/img/slide_1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}

The process began by identifying which annotations should be used to assess each of the system’s accuracy from. The authors considered HIPAA’s Privacy Rule “Safe Harbor” method which consists of eighteen categories of PII that the de-identification system would need to target. However, since the three systems were not all designed to address all PII categories, the categories were divided into two sets: shared categories that all three systems targeted and specialty categories which only two of the systems targeted. Accuracy was determined for both individual PII categories as well as PII as a whole, that is, a system could wrongly identify the PII category but would still count as true positive for identifying that it was PII.

Next, they determined the reference corpora to use which were the 2014 and 2016 i2b2 de-identification challenge corpora, both of which were publicly available. The 2014 corpus was split into 790 training notes and 514 test notes, and the 2016 corpus was split into 200 development notes, 600 training notes, and 400 test notes. The notes in the 2016 corpus tended to be longer with an average of 1,863 words per note versus 617 words per note in the 2014 corpus.

Both corpora were processed as plain text files with one note per file and all three of the de-identification systems were tested out-of-the-box.

{% include figure.liquid loading="eager" path="assets/img/slide_2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}

Slide 3:
The paper then discusses the three text de-identification systems that would be evaluated. The first is Amazon Comprehend Medical which is a cloud-based natural language processing system. For this system, they focused on the detect phi service endpoint, which can be run using API calls or remotely on an AWS instance. To test the system, they used a simple Python script to read in a note, post it to the service endpoint, and then convert the returned output to the brat standoff format.
The next system was Clinacuity’s CliniDeID. The on-premises version can use a graphical user-interface or the command-line, though in the paper they used the command line. This system offers multiple levels of de-identification, so they chose the ‘Beyond HIPAA Safe Harbor’ level because it better aligned with the categories of the other systems. Testing was done using a special testing license.
The third system was the National Library of Medicine’s Scrubber. This system is also on-premises and can be used through either a graphical user-interface or the command-line. This system outputs a redacted version of the original note. However, since the other systems output annotated offsets or the reference corpus, they needed to write a script to map the NLM Scrubber’s output file to the annotation format by lining up the preceding and following context around all bracketed redacted forms.
To generate accuracy metrics for the systems, they used ETUDE (Evaluation Tool for Unstructured Data and Extractions). This tool evaluates each of the reference and system documents based on corpus specific configuration files. They also used a partial matching flag to evaluate annotations, meaning that as long as two annotations matched categories and their spans at least partially overlapped it would be considered a true positive.

{% include figure.liquid loading="eager" path="assets/img/slide_3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}

Slide 4:
Next, I can talk about the results. So, the National Library of Medicine’s Scrubber was by far the fastest. It was about twice as fast at processing ten thousand characters as compared to Amazon Comprehend and about 14 times faster than CliniDeID. The NLM Scrubber was also much better at processing more characters per second as compared to the two other systems. But the NLM Scrubber failed to process four notes which was due to non-ASCII characters being present. Amazon Comprehend also did not process thirty-five notes, which ended up being the thirty-five longest notes, so this could be an opportunity for this system to improve its timing.

{% include figure.liquid loading="eager" path="assets/img/slide_4.jpg" title="example image" class="img-fluid rounded z-depth-1" %}

Slide 5:
As for accuracy, we can see that CliniDeID performed substantially better than the other two systems. Amazon Comprehend tended to perform better than the NLM Scrubber except for the address category, though overall Amazon Comprehend and the NLM Scrubber tended to perform relatively similarly. CliniDeID had challenges with the eAddress and ID categories and the NLM Scrubber had difficulties with the age category.

{% include figure.liquid loading="eager" path="assets/img/slide_5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
