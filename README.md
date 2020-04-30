# N-Hance System Recreation for SemEval 2017 Task #7
Created by Cameron Knopp & Jorge Mazariegos

This is a recreation of the N-Hance pun detection system, which was created to solve task 7 of Semeval-2017. The ultimate goal of this system is Word Sense Disambiguation (WSD) of a pun word given its context. You must download the following dataset in order to be run this project:
  - wiki-news-300d-1M.magnitude
    Found here: http://magnitude.plasticity.ai/word2vec/medium/GoogleNews-vectors-negative300.magnitude 
    
    
This system provides solutions to three subtasks:

# Subtask 1: Pun detection.
For this subtask, participants are given an entire raw data set. For each context, the system must decide whether or not it contains a pun.

# What we did for this subtask
- Create word_pairs for sentences in given file
- Calculate pmi scores for all given word_pairs
- Calculate the interquartile range for the pmi scores of word_pairs in each sentence
- Find the median value of the interquartile ranges across all sentences in the given dataset
- For each sentence, if the highest pmi score - second highest pmi score > median interquartile range then that sentence contains a pun


# Subtask 2: Pun location.
For this subtask, the contexts not containing puns are removed from the data set. For each context, the system must identify the pun word.


# What we did for this subtask
- Generate pmi scores for the given sentence
- The second word in the word pair with the highest pmi score in a given sentence is the pun word


# Subtask 3: Pun interpretation.
For this subtask, the pun word in each context is marked, and contexts where the pun's two meanings are not found in WordNet are removed from the data set. For each context, the system must annotate the two meanings of the given pun by reference to WordNet sense keys.

# What we did for this subtask
- First sense of the pun is found using pywsd algorithm
- To find the second sense of the pun, gather all the wordnet synonyms of the pun
- Next, get the other word in the highest pmi score word pair which the pun belongs to. We'll call this the target word.
- Use the pymagnitude word2vec to find the cosine similarity between each of the synonyms and the target word.
- The synonym with the highest cosine similarity to the target word is the second sense of the pun word.


# Where to find our system's output from the subtasks
The output of our system for the 3 subtasks can be found in the "system_output" folder. 

# Scorer results and running the scorer
The results of running the scorer for our system on each of the 3 subtasks can be found within the "system_results" folder. Details on how to run the scorer are found in the README.md file within the "datasets" folder.

# References
Miller, T., Hempelmann, C., & Gurevych, I. (2017). SemEval-2017 Task 7: Detection and Interpretation of English Puns. Proceedings of the 11th International Workshop on Semantic Evaluation. doi: 10.18653/v1/s17-2005

Sevgili, Ö., Ghotbi, N., & Tekir, S. (2017). N-Hance at SemEval-2017 Task 7: A Computational Approach using Word Association  for Puns. Proceedings of the 11th International Workshop on Semantic Evaluation. doi: 10.18653/v1/s17-2074
