# Learning Semantic Correspondences

* **grounded language acquisition:** learning the meaning of sentences in the context of an observed world state

## Challenges

* **multiple ambiguities**
	(1) **text segmentation:** the segmentation of the text into utterances
	(2) **fact identification:** the identification of relevant facts, i.e., the choice of records and aspects of those records
	(3) **alignment:** the alignment of utterances to facts (facts are the meaning representations of the utterances)
* **Noise:** Furthermore, in some of our examples, much of the world state is not referenced at all in the text, and, conversely, the text references things which are not represented in our world state.

## Method

* **unified framework** for text segmentation, fact identification, and alignment
* The parameters of this **hierarchical hidden semi-Markov model** can be estimated efficiently using **EM**
* **scenario:** pair of text *w* and the world state *s* it describes

## Generative Model

* three stages:
	1. Record choice
	2. Field choice
	3. Word choice
	
### Record choice

* capture two types of regularities:
	1. salience (prominence)
	1. coherence (order of mentions)