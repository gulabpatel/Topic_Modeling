# Topic_Modeling

🔥Topic Modelling: Intentionally short primer and A mental model.

👉 Criteria A: Discover topics in a corpus with long-form docs of size: small to medium & you are open to dealing with cleanup (stop words), muck with hyper-parameters & involve HITL to assign readable topics.

- Use cases: Analyse employee emails (long-form) to understand the top N topics that lead to mass resignations.

- 2 Options: Matrix factorisation (MF)-based & Probabilistic sampling-based.

- Mode: Unsupervised

A variant of MF: Decompose a term-doc frequency matrix A into W & H (in W, all rows (i) are docs & cols (j) are words, in H, all rows are words & cols are topics). Imagine Wij. Hjk. K is the number of topics & it is manually chosen. Idea is to reduce i.e ||A-W.H||. If SVD is used for MF then it’s LSA. The probabilistic variation of it is pLSA. Another variation of pLSA is NMF.

But if you do this probabilistically using sampling tech like Gibbs sampling then it’s LDA.

✅Pros: The topics are open for good human interpretations.

❌Cons: By default word is the tactical unit, word order & context are ignored (Though you could play with the ngram range while generating a term-doc matrix, it’s still a BoW). You are also at the mercy of the implementation, I have “heard” Mallet is “decent”. Finally, Can’t handle a huge corpus.

👉 Criteria B: Discover topics in a corpus of long or short texts & you don’t want to deal with corpus cleanup, a lot of hyper-parameters, leveraging SoTA LMs with some convenient features.

- Use cases: Prev use-case + Analyse Trump tweets to understand the topics during the Capitol invasion

- 2 Options: Top2vec & BERTopic

- Mode: Top2vec (Unsupervised) & BERTopic (can do supervised, semi/guided & DTM).

Both follow the same 5 steps, vectorize docs using algorithms (in the likes of Doc2Vec all the way up to Transformers), lower dimensions of docs using UMAP, make clusters using HDBSCAN, calculate centroids (which is the topic) & get Top N similar or closer docs to the centroids. But BERTopic varies in the last 2 steps (which is its weakness) & in the list of vectorization algorithms it supports. Ref the papers for more.

✅Pros: Both have some nice bells & whistles like search & Viz. The results show both works better with short texts with better coherence & diversity. SoTA vectorization algorithms take care of topic & doc semantics.

❌Cons: High-quality doc vectors come at a price & can be very slow. The main drawback of BERTTopic is that even though docs are vectorized using semantic vectors the topics are still vectorized using a variant of a BoW called c-TF-IDF. This is still a challenge.

👉 Criteria C: Your docs are represented by many *correlated* topics. Go for variational inference-based CTM - Correlated topic models. Fx BERTopic assumes "A doc pertains to one topic more than others" but it is far from reality in certain domains.
