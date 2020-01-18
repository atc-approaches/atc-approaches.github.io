# Automatic Text Classification Methods

You can use the [editor on GitHub](https://github.com/atc-approaches/atc-approaches.github.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

## 2-Pass Methods

### TFIDF 
The simplest and almost universally used approach in which a document is represented as term vector with TFIDF weights of terms as elements. TFIDF$_i$ of element $i$ in the vector is given by  TF$_i$ $\times$ IDF$_i$, where TF$_i$ is the frequency of term $i$ in the document and  IDF$_i = log(\frac{N}{df_i})$, where $N$ is total number of documents and $df_i$ is the document frequency of the i-th term.

### Metafeatures

Strategies based on Metafeatures (MFs) extract information from other more basic features (such as TFIDF) aiming at improving the feature space based on the main assumption that close documents tend to belong to the same class. The MFs we exploit here are the most effective ones according to~\citet{tkde}. We adopt the combined use of the similarity scores (cosine and $l2$) between a document and each category centroid as meta-features that exploit global information, and the similarity between a document and its neighbors from each category as meta-features that exploit local information. We also complement the aforementioned meta-features using the recently proposed ones that indicate hard-to-classify target documents~\cite{CanutoSIGIR19}. Such meta-features evaluate the proportion of correctly classified (using the SVM classifier) neighbors of a target document, and the discrepancy between the classification of a target document and its neighbors. Our implementation of the MF approach was obtained from the authors of the original work, based on direct communications.

## End-To-End Methods

### FastText
FastText learns vectors for character n-grams found within each word, as well as for the complete word. At each training step in FastText, the mean of the target word and subword vectors are used for training. The adjustment that is calculated from the error is then used uniformly to update each of the vectors that were combined to form the target. This adds a lot of additional computation cost to the training step. The trade-off is a set of word-vectors that contain embedded sub-word information. In~\cite{joulin2016fasttext}, the authors presented a supervised version of FastText word and document representation\footnote{Our implementation of FastText was obtained from \url{https://fasttext.cc/}.}, which used the hierarchical softmax as loss function to approximates the softmax with a much faster computation. The idea is to build a binary tree whose leaves correspond to the labels. As an additional experiment, we also use document vectors as input to train a linear classifier, which was chosen SVM.


### CNN
The convolutional architecture we exploit in our comparative work deals with document classification at character-level using embeddings of characters~\cite{NIPS2015_5782}. This architecture showed excellent results for the ATC task in the authors' experimental evaluation \cite{NIPS2015_5782, xiao2016efficient}. The CNN architecture is very straightforward  -- it contains nine deep layers (6 convolutional and 3 fully connected layers) considering $1024$ kernel filters. Its character alphabet consists of $70$ characters with feature length of $1014$, with a  dropout of $0.5$ in between fully connected layers\footnote{\label{note1}. The  Implementation of CNN, VDCNN and HAN are available at  \url{https://github.com/ArdalanM/nlp-benchmarks}}.

## References

