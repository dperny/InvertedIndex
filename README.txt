Problem: given a file where each new line is a new document, output the number
of times each word occurs in each document and the number of documents it 
occurs in.

Glossary: 

  Document
  - One line from a larger file consisting of words.

  Document number (Docno) 
  - the byte-offset in the orig. file of the location of the line

  Document frequency (df)
  - the number of documents a word appears in

  Term frequency (tf)
  - the number of times a word appears in a document

  Posting
  - a (docno, tf) pair
  
  Postings list
  - a df followed by a list of Postings

Map Stage:

  Input: docno -> document
    For each word, output the word and the docno it occurs in
  Output: Word -> docno

Reduce Stage:

  Input: Word -> (List of docnos)
    for each docno
      if the docno not yet in the postings list
        add new posting to postings list with tf = 1
      else
        increment the tf of the posting with this docno already in the list
    set df = length (postings list)
    
  Output: Word -> (df, Posting)
