# Semantic Distracotor Generator

Data used in my 2013 ACL paper, "Discriminative Approach to Fill-in-the-Blank Quiz Generation for Language Learners"

Keisuke Sakaguchi (keisuke-sa[at]is.naist.jp)  
Last updated: May 29th, 2013


- - -
This document describes the proposed method (DiscSimESL) described in my 2013 ACL paper:

    N.B. This is a tentative information.
    @InProceedings{TBD,
    author    = {Sakaguchi, Keisuke and Arase, Yuki and Komachi, Mamoru}
    title     = {Discriminative Approach to Fill-in-the-Blank Quiz Generation for Language Learners},
    booktitle = {Proceedings of the 51th Annual Meeting of the Association for Computational Linguistics},
    month     = {August},
    year      = {2013},
    address   = {Sofia, Bulgaria},
    publisher = {Association for Computational Linguistics},
    pages     = {TBD},
    url = {TBD}
    }

It includes data and code used to generate a fill-in-the-blank quiz with a semantic distractor for a given sentence which contains a target word.
In this code we focus on 689 major verbs extracted from the Lang-8 Corpus as targets.

N.B.

- There are 689 target verbs extracted from the Lang-8 Corpus, but the DiscSimESL covers 679.
- It does not include the original Lang-8 and VOA (Voice of America) data due to licensing restrictions.
- We have checked that the code runs on Linux (Ubuntu 12.04.2 LTS).

## Pre-requisites
Some Python modules are required to run the program.

1. [lxml](http://lxml.de/)
2. [numpy](http://www.numpy.org/)
3. [scikit-learn](http://scikit-learn.org/stable/)
4. [pattern.en](http://www.clips.ua.ac.be/pages/pattern-en)

## Procedure
1. Download my code for generating semantic distractors, which is available at Github.
    `` git clone git@github.com:keisks/disc-sim-esl.git ``

        > tree -L 1
         .
        ├── README.md    #This file
        ├── classifiers  #Classifiers for each verb.
        ├── data         #Confusion matrix
        ├── generate.py  #Main script
        ├── quiz_src     #Source files for quizzes
        ├── sample.txt   #Sample text file for a quiz.
        └── scripts      #Sub scripts

2. Parse *.txt file that contains sentences for quizzes. We use [Stanford CoreNLP](http://www-nlp.stanford.edu/software/corenlp.shtml) and put the output xml file into quiz_src/xml directory. N.B. The dcoref option is not necessary. 


        Input: sample.txt  
        Run: java -cp stanford-corenlp-1.3.5.jar:stanford-corenlp-1.3.5-models.jar:xom.jar:joda-time.jar:jollyday.jar -Xmx3g edu.stanford.nlp.pipeline.StanfordCoreNLP -annotators tokenize,ssplit,pos,lemma,ner,parse -file sample.txt -outputDirectory quiz_src/xml/  
        Output: quiz_src/xml/sample.txt.xml


3. Execute generate.py to generate quiz sentences and options.
 This script will produce quiz sentences in quiz_src/questions, and quiz options in quiz_src/distractor_answer.

        Run: python generate.py
        Output:  
        quiz_src/questions/sample.question  
        quiz_src/questions/sample.answer


## ToDo
- Script to generate quiz in a test booklet style.
- Checking availability on Windows.

- - -
If you have any questions, please email me.

