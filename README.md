# Semantic Distracotor Generator

Data used in my 2013 ACL paper, "Discriminative Approach to Fill-in-the-Blank Quiz Generation for Language Learners"

Keisuke Sakaguchi (keisuke[at]cs.jhu.edu)  
Last updated: October 12th, 2013

Note: The code is outdated and needs to be updated to be compatible with recent packages. Sorry for the inconvenience!

- - -
This document describes the proposed method (DiscSimESL) described in my 2013 ACL paper:

    @InProceedings{sakaguchi-arase-komachi:2013:Short,
    author    = {Sakaguchi, Keisuke  and  Arase, Yuki  and  Komachi, Mamoru},
    title     = {Discriminative Approach to Fill-in-the-Blank Quiz Generation for Language Learners},
    booktitle = {Proceedings of the 51st Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers)},
    month     = {August},
    year      = {2013},
    address   = {Sofia, Bulgaria},
    publisher = {Association for Computational Linguistics},
    pages     = {238--242},
    url       = {http://www.aclweb.org/anthology/P13-2043}
    }

It includes data and scripts to generate a fill-in-the-blank quiz with a semantic distractor for a given sentence which contains a target word.
We focus on 689 major verbs extracted from the Lang-8 Learner Corpora (http://cl.naist.jp/nldata/lang-8/) as targets.

N.B. 

- There are 689 target verbs extracted from the Lang-8 Corpus, but the DiscSimESL covers 679.
- It does not include the original Lang-8 and VOA (Voice of America) data due to licensing restrictions.
- We have checked that the code runs on Linux (Ubuntu 12.04.2 LTS) and Windows 7 (x64).
- Classifiers for K-best quiz generation are not uploaded due to the data size (=18G). If you are interested in, please e-mail me.

## Pre-requisites
The scripts basically run on Python(2.7+).  
Some Python modules and the [Stanford CoreNLP](http://www-nlp.stanford.edu/software/corenlp.shtml) toolkit are necessary to run the program.

1. [lxml](http://lxml.de/) 
2. [numpy](http://www.numpy.org/)
3. [scikit-learn](http://scikit-learn.org/stable/)
4. [pattern.en](http://www.clips.ua.ac.be/pages/pattern-en)

N.B. 
For Windows (x64) users, you may download Python [here](http://www.python.org/getit/) and find x64 extension packages for lxml and scikit-learn [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/). Currently, easy_install, pip, etc. don't support these python modules for Windows (x64).


## Procedure
1. Download my code for generating semantic distractors, which is available at Github. If you are not familiar with git/github, please install git following the instruction [here](http://git-scm.com/book/en/Getting-Started-Installing-Git).

    `` git clone git@github.com:keisks/disc-sim-esl.git ``   
    or  
    `` git clone https://github.com:keisks/disc-sim-esl.git ``  
    or  
    You can download the zip file on the right side.
  

        > tree -L 1
            .
           ├── README.md         # This file
           ├── classifiers       # Classifiers for each verb
           ├── classifiers_kbest # K-best classifiers for each verb (blank)
           ├── data              # Confusion matrix
           ├── generate.py       # Main script
           ├── generate_kbest.py # Main script for K-best output
           ├── quiz_src          # Source files for quizzes
           ├── sample.txt        # Sample text file for a quiz
           └── scripts           # Subscrips


2. Parse *.txt file that contains sentences for quizzes. We use [Stanford CoreNLP](http://www-nlp.stanford.edu/software/corenlp.shtml) and put the output xml file into quiz_src/xml directory. (The dcoref option is not necessary.)

        Input: sample.txt  
        Run: java -cp stanford-corenlp-1.3.5.jar:stanford-corenlp-1.3.5-models.jar:xom.jar:joda-time.jar:jollyday.jar -Xmx3g edu.stanford.nlp.pipeline.StanfordCoreNLP -annotators tokenize,ssplit,pos,lemma,ner,parse -file sample.txt -outputDirectory quiz_src/xml/  
        Output: quiz_src/xml/sample.txt.xml



3. Edit the path for pattern.en in generate.py (line 18)

        Edit path_to_pattern = "YOUR_PATH_TO_pattern.en (e.g. ./pattern-2.4/)"


4. Execute generate.py to generate quiz sentences and options.
 This script will produce quiz sentences in quiz_src/questions, and quiz options in quiz_src/answer_distractor.

        Run: python generate.py or generate_kbest.py
        Output:  
        quiz_src/questions/sample.question  
        quiz_src/questions/sample.answer
        quiz_src/answer_distractor/sample.txt.ans_dist
        quiz_src/answer_distractor/sample.txt.ans_dist_kbest
        (Kbest distractors are ranked by log-probability.)
        

- - -
If you have any questions, please email me (keisuke[at]cs.jhu.edu).

