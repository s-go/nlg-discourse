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

* choose a sequence of records to describe
* capture two types of regularities:
	1. salience (prominence)
	1. coherence (order of mentions

### Field choice

* for each chosen record, select a sequence of fields

### Word choice

* for each chosen field, choose a number and generate a sequence of words
* Note that since their model always observes the words, this simplistic representation at the surface level is adequate (however, relaxing the independence assumption, e.g., by additionally conditioning on the previous word(s), could potentially yield a more powerful model)
(Konstas/Lapata 2013: 311)
* Their model supports three different types of fields, namely string, categorical and integer. For each
of those they adopt a specific generation strategy at the word level.

# Usage in Generation

* Kim and Mooney (2010) address this problem by interfacing the alignments with WASP−1 (Wong & Mooney, 2007). The latter is a publicly available generation system which takes an alignment as input and finds the most likely string using the widely popular noisy-channel model.
* Angeli et al. (2010) propose a model different in spirit which nevertheless also operates over the alignments of Liang et al. Using a template extraction method, they post-process the alignments in order to obtain a sequence of records, fields, and words which are spanned by the chosen records and fields.
* Konstas, I., & Lapata, M. (2013). A global model for concept-to-text generation. Journal of Artificial Intelligence Research, 48, 305346.