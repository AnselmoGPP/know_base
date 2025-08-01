# Information retrieval

<br>![miscellany image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/miscellany.jpg)

## Table of Contents
+ [References](#references)
+ [Boolean retrieval](#boolean-retrieval)
+ [The term vocabulary and postings list](#the-term-vocabulary-and-postings-list)
+ [Dictionaries and tolerant retrieval](#dictionaries-and-tolerant-retrieval)
+ [Index construction](#index-construction)


## References

- Manning, C.D., Raghaven, P., & Schütze, H. (2009). _**An Introduction to Information Retrieval**_ (Online ed.). Cambridge, MA: Cambridge University Press. Retrieved from [here](http://nlp.stanford.edu/IR-book/information-retrieval-book.html)


## Boolean retrieval

**Information retrieval (IR):** It’s finding material (usually documents) of an unstructured nature (usually text) that satisfies an information need from within large collections (usually stored on computers). IR is becoming the dominant form of information access, overtaking traditional database-style searching (relational databases are structured data). It’s used in web search engines, email searching, documents browsing/filtering/processing (it involves clustering/grouping documents), etc.

IR systems can be distinguished by the scale at which they operate:

- Web search: Search over billions of documents. Documents are gathered for indexing.
- Enterprise, institutiona, and domain-specific search: Search of corporation’s internal documents, database of patents, research articles, etc.
- Personal IR: Search within the OS or email.

Let’s use “Shakespeare’s Collected Works” as an example.

**Linear scanning** (grepping through text): Linear scan through documents searching something (like the Unix command grep). Simplest form of document retrieval. Useful for simple querying of modest collections (get Shakespeare’s plays containing the words Brutus AND Caesar AND NOT Calpurnia). However, this is not enough for processing large document collections quickly (online data), allowing more flexible matching operations (get plays containing the word Romans and countrymen within the same sentence), or allowing ranked retrieval (get best answer).

**Indexing:** We can avoid linearly scanning texts for each query by indexing them in advance. We can record for each document (each Shakespeare’s play) whether it contains each word out of all the words (Shakespeare) used, which produces a binary term-document incidence matrix.

**Boolean retrieval model:** Model in which we can pose any query which is in the form of a Boolean expression of terms (i.e., in which terms are combined with the operators AND, OR, NOT).

- **Terms:** The indexed units (usually words).
- **Documents:** The units we build a retrieval system over.
- **Collection/Corpus:** Group of documents over which we perform retrieval.

**Ad-hoc retrieval:** A system aims to provide documents from within the collection that are relevant to an arbitrary user information need, communicated to the system by means of a one-off, user-initialized query. It’s the most standard IR task.

**Information need:** Topic about which the user desires to know more.

**Query:** What the user conveys to the computer in an attempt to communicate the information need.

**Relevance:** A document is relevant if the user perceives it as containing information of value with respect to their personal information need.

**Effectiveness:** The effectiveness of an IR system depends on the quality of its search results. To know the effectiveness, we need to know the precision and recall of the system’s returned results for a query:

- **Precision:** What fraction of the returned results are relevant to the information need?
- **Recall:** What fraction of the relevant documents in the collection were returned by the system?

We have to build a term-document matrix by only recording the things that do occur (the ones) because about 99.8% of cells are zero.

**Inverted index:** Dictionary of terms (vocabulary or lexicon). For each term, we have a list (postings list or inverted list) that records which documents the term occurs in. Each item in the list is a posting. It’s useful to sort the dictionary (alphabetically) and the postings lists (by docID) for more efficient query processing.

The index has to be built in advance for improving retrieval time:

- Collect the documents to be indexed.
- Tokenize the text: Turn each document into a list of tokens (pair token-docID).
- Do linguistic preprocessing: Sort each token. Multiple occurrences of the same term from the same document are merged.
- Index the documents that each term occurs in (create the inverted lists): Group instances of the same term and create a dictionary entry (term + postings).
- Now we have an Inverted index (indexing terms + inverted lists).

**DocID:** Within a document collection, each document must have a unique serial number (document identifier). During index construction, we can assign successive integers to each new document when it’s first encountered.

The dictionary also records some statistics like document frequency (number of documents containing each term, or length of the postings list). This data is not vital, but helps improve efficiency of the search engine at query time, and it is used in many ranked IR models.

This inverted index structure is the most efficient structure for supporting ad-hoc text search.

Postings lists are much larger than the indexing terms. The terms are commonly kept in memory, while postings lists are kept on disk. Good data structure options for in-memory postings lists are:

- Singly linked lists: Cheap insertion.
- Variable length arrays: No pointers overhead and faster traversing. Useful if updates are infrequent.
- Hybrid scheme: Linked list of fixed length arrays for each term.

When postings lists are stored on disk, they’re stored as a contiguous run of postings without explicit pointers, so as to minimize the postings list size and the number of disk seeks to read a postings list into memory.

How to process a query using an inverted index and the basic Boolean retrieval model (example: process the simple conjunctive query Brutus AND Calpurnia):

1 Locate Brutus in the dictionary > Retrieve its postings
2 Locate Calpurnia in the dictionary > Retrieve its postings
3 Find documents containing both terms by **intersecting** both postings lists (merge algorithm). You can do this by traversing both postings lists simultaneously (linear time), advancing over the smaller docID.

**Query optimization:** Process of selecting how to organize the work for answering a query so that the system makes the minimum amount of work. This is useful in more complex queries (example: (Brutus OR Caesar) AND NOT Calpurnia). For arbitrary Boolean queries, we have to evaluate and temporarily store the answers for intermediate expressions in a complex expression.

**Vector space model:** Type of ranked retrieval model. A set of words is used (instead of querying using a language with boolean operators: AND, OR, NOT) and the system decides which document satisfy the query.

**Extended Boolean retrieval model:** It incorporates additional operators (apart from AND, OR, NOT) such as term proximity operators.

**Proximity operator:** It specifies that two terms in a query must occur close to each other in a document. Closeness may be measured by limiting the allowed number of intervening words or by reference to a structural unit (sentence, paragraph…).

Boolean queries are precise, offering the user greater control and transparency. However, free text queries produce better results than Boolean queries (Turtle, 1994). Using AND operators produce high precision but low recall, while using OR gives low precision but high recall, and it’s almost impossible to find a satisfactory middle ground.

Additional things we desire:

- Better determining terms, providing tolerance to spelling mistakes and inconsistent choice of words.
- Search for compounds or phrases that denote a concept. We can augment index for capturing the proximities of terms in documents (operating + system, Microsoft + Gates…).
- Give more weight to documents that have a term more times than others. This requires term frequency information in postings lists.
- Order (rank) the retrieved documents depending upon a score that says how good it matches the query.


## The term vocabulary and postings list

### Document delineation and character sequence decoding

Digital documents that are the input to an indexing process are typically bytes in a file, so we have to convert this byte sequence into a linear sequence of characters. This is easy for plain English in ASCII encoding, but is complex for other encoding schemes (Unicode UTF-8, etc.). 

    Obtaining the character sequence in a document
    Choosing a document unit 


### Determining the vocabulary of terms

    Tokenization
    Dropping common terms: stop words
    Normalization (equivalence classing of terms)
        Accents and diacritics.
        Capitalization/case-folding.
        Other issues in English.
        Other languages. 
    Stemming and lemmatization 


### Faster postings list intersection via skip pointers
### Positional postings and phrase queries

    Biword indexes
    Positional indexes
        Positional index size. 
    Combination schemes 





## Dictionaries and tolerant retrieval

## Index construction




















1) How can the given dictionary be helpful for spelling corrections in Doc1? 


That dictionary can be helpful for spelling corrections in Doc1 by serving as a reference to identify and correct misspelled words. It can be used for identifying misspelled words (by comparing each word in Doc1 against the words in the dictionary, it's possible to identify which words are misspelled or not present in the dictionary) and correcting them (for each misspelled word identified in Doc1, the correct spelling can be retrieved from the dictionary and replaced in the text). Result: "At Mount Everest, 12 people were lost. This [information] about [jeopardy] raised fear".

2) Describe the approach used to correct the spellings of ‘information’ and ‘jeopardy’ in the Doc1 using Levenshtein distance and k-gram overlap (you may choose the value of k). Create a table to compute the edit distance using Levenshtein distance metric among the pair of strings. 

First, let's get the Levenshtein distance (minimum number of single-character edits required to change one word into another) between each misspelled word in Doc1 and the correct words in the dictionary.

- "inforomation" - "information": The Levenshtein distance is 3 (replace 'r' with 'm', add 'm', add 't')
- "jopardy" - "jeopardy": The Levenshtein distance is 1 (replace 'a' with 'e')

Now, let's get the k-gram overlap (similarity between two strings based on the number of k-grams, subsequences of length k, they share). 
We choose k=2 and compute the k-grams for each misspelled word in Doc1 and the correct words in the dictionary.

- "inforomation": The k-grams are ['in', 'nf', 'fo', 'or', 'ro', 'om', 'ma', 'at', 'ti', 'io', 'on']
- "information": The k-grams are ['in', 'nf', 'fo', 'or', 'rm', 'ma', 'at', 'ti', 'io', 'on']
- Common k-grams: ['in', 'nf', 'fo', 'or', 'ma', 'at', 'ti', 'io', 'on']
- k-gram overlap (number of common k-grams) = 9

- "jopardy": The k-grams are ['jo', 'op', 'pa', 'ar', 'rd', 'dy']
- "jeopardy": The k-grams are ['je', 'eo', 'op', 'pa', 'ar', 'rd', 'dy']
- Common k-grams: ['eo', 'op', 'pa', 'ar', 'rd', 'dy']
- k-gram overlap = 6

Then, let's get the edit distance table:
"information"	"jeopardy"
"inforomation"	3	-
"jopardy"	-	1

We can choose the correct word with the lowest edit distance for each misspelled word in Doc1. Here, "information" has the lowest edit distance for "inforomation," and "jeopardy" has the lowest edit distance for "jopardy".

3) In this situation, the dictionary is sorted. If the dictionary is not sorted, what shall be its impact on the process chosen by you in Q2?

If the dictionary is not sorted, it can have an impact on the efficiency of the spelling correction process. Sorting the dictionary can significantly improve the speed of searching and matching during the spelling correction process.

- For Levenshtein distance, the algorithm would need to compare the misspelled word with every entry in the dictionary, leading to a higher time complexity (sorting it allows for more efficient searching, reducing the number of comparisons needed).

- For k-gram overlap, the algorithm may need to compute k-grams for each misspelled word and compare them against all entries in the unsorted dictionary, leading to higher computational complexity. Sorting the dictionary based on k-grams could facilitate faster searching and matching.





