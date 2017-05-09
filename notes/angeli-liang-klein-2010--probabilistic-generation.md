# Angeli et al. (2010)

* Angeli, G., Liang, P., & Klein, D. (2010). A simple domain-independent probabilistic approach to generation. In Proceedings of the 2010 Conference on Empirical Methods in Natural Language Processing, pp. 502-512, Cambridge, MA.

## Overview

* We use the model of **Liang et al. (2009)** to automatically induce the correspondences between words in the text and the actual database records mentioned.
* We break up the full generation process into a sequence of local decisions, training a **log-linear classifier** for each type of decision.
* three types of decisions:
	1. **macro content selection** chooses records from the database (*record decisions*)
	2. **micro content selection** chooses a subset of fields from a record (*field set decisions*)
	3. **surface realization** chooses a suitable template to render the content (*template decisions*)

* each decision is allowed to depend **on the entire history** of previous decisions

## The Generation Process

* Domain-independent **feature templates** govern the record, field set, and template decisions.
* Feature templates are represented as functions of the current decision and past decisions. They can, in general, depend on the current decision and *all* previous decisions.

### Template decisions

* After T~i~ has been chosen, each field in the template is replaced with a word given the corresponding field value in the world state (see Liang et al. 2009).

## Learning Model

### Model

* probability model (1)
* chaining of log-linear models for each decision (2)
* The ability to condition on arbitrary histories is a defining property of these models.

### Using the Model for Generation

* In our experiments, we choose `d` by sequentially choosing the best decision in a greedy fashion (3)

### Learning

* maximize objective function (4) with L-BFGS

#### Latent Alignments

* our training data includes only the world state `s` and generated text `w`, not the full sequence of decisions `d` needed for training
* We use the model of Liang et al. (2009) to impute the decisions `d`.
	* latent alignment specifies (1) the sequence of records that were chosen, (2) the sequence of fields that were chosen, and (3) which words in the text were spanned by the chosen records and fields
	* This information specifies the record decisions and a set of fields for each record.

#### Template Extraction

* For each record, an aligned training scenario specifies a sequence of fields and the text that is spanned by each field.
* We create a template by abstracting fieldsthat is, replacing the words spanned by a field by the field itself (COARSE template)
	* The problem with using this template directly is that fields can be noisy due to errors from the unsupervised model
* Therefore, we also create a BASE template which only abstracts a subset of the fields
	* we define a *trigger pattern* which specifies a simple condition under which a field should be abstracted, e.g.
		* numbers
		* wind directions
		* names
		* ...