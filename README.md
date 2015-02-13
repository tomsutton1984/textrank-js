textrank-js
===========

TextRank is an algorithm for Text Summarization, by Rada Mihalcea & Paul Tarau.  This code here is based on their paper "TextRank: Bringing Order into Texts".  I've noticed that there are many implementations out there, but this one is intended to demonstrate the algorithm without any additional baggage.  I wanted to show how elegant, simple and clean it is, so here is an implementation in about ~130 lines of Javascript (ES5).  It currently depends on lodash for a single function.  This could easily be modified to make it dependency free if the ES6 find function exists, or by a slight code mod to that line.

The algorithm itself can extend to any type of graph, as they note in their paper, but I have provided two types of graphs explored in the paper: keyword extraction with an undirected graph derived from collocation, and sentence extraction using the similarity weighting on the edges in an undirected graph.  There is a method in the module for each type, and once the graph has been built, the textRank function performs the algorithm on the generated graph.

Note this code only implements the TextRank algorithm itself, the sentences must be properly formatted upfront.  I have provided example tokenization for both tasks in the tests directory, both derived from tokenizing the Wikipedia entry for "Automatic summarization", both minimally processed using a custom (very minimal) tokenizer, and OpenNLP's default models for sentence splitting and POS, and converted to JSON.  As long as you get the format right that this is expecting, you should be able to use whatever library you want to preprocess.  The keyword extraction builder needs the format to include POS tags since it filters the content while it is building its adjacencies.  The sentence extraction builder does not require POS, but requires pre-split sentences.

The "tests" are not currently testing anything, but serve as demonstration code for how to run the software.  Note that textRank() has a default number of iterations -- it doesnt try and test for convergence.  This is just to keep it simple, it would be simple to modify to test this instead, but for now you can pass in any number you want if that default isnt suitable (see test examples).

Build using Grunt:
```
$ npm install
$ grunt

```

You are welcome to use this code for whatever nefarious purposes, but please attribute it to this implementation if you do.
