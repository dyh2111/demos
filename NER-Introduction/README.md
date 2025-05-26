# NER – Named Entity Recognition, an Introduction

By Dan Harvey  

📧 dan \[at] danielyusay.com
📧 daniel.harvey \[at] columbia.edu

---

Named Entity Recognition (NER) is the task of locating and classifying entities (words + phrases) within typically unstructured text into defined categories such as persons, organizations, locations, dates, and more. Originally formalized at the Sixth Message Understanding Conference (MUC-6), NER has evolved from recognizing proper nouns for NLP research into information extraction and document structuring within modern NLP and machine learning pipelines such as RAG.

Modern NER is foundational for population of structured or knowledge databases, search engine enhancement, document categorization, question answering systems, chatbots, and entity linking. It is also integral to modern hybrid systems like Retrieval-Augmented Generation (RAG) and GraphRAG, where structured entities guide semantic search and query generation.

---

## History of NER

My initial exposure to NER began during my undergraduate studies in COMS4705 Natural Language Processing with Professor Daniel Bauer, where we started with early systems that relied heavily on handcrafted and rule-based grammars. These early methods used regex, context-free grammars (CFGs), probabilistic CFGs (PCFGs), and semantic role labeling techniques like PropBank and FrameNet. While these were interpretable and heavily based in formal linguistics, these systems struggled to scale.

The limitations of these methods led to the adoption of statistical learning frameworks. Models such as Hidden Markov Models (HMMs), Maximum Entropy classifiers, and particularly Conditional Random Fields (CRFs) became dominant. These probabilistic models allowed for more robust sequence labeling, leveraging both the local context and dependencies between output labels. One of the foundational contributions during this time was the introduction of the BIO tagging scheme by Ramshaw and Marcus (1995), which systematized the annotation of entity spans using prefix tags to denote beginnings, insides, and non-entities. BIO remains the backbone of most modern NER datasets and evaluation protocols even to this day.

With the rise of deep learning, where neural networks began to model sub-word features and orthographic patterns. CNNs worked well at extracting character-level patterns and were typically used in combination with word-level models and token representations. The combination of Bidirectional LSTMs with CRFs soon followed, enabling more contextual modeling and improved decoding. This architecture became the standard baseline for NER tasks for several years thanks to its ability to capture sequential context and enforce valid tags.

Naturally, transformer models dramatically shook up the landscape. BERT and its flavors, particularly RoBERTa, brought SOTA performance to NER by using deep contextual embeddings derived from self attention. RoBERTa improved upon BERT by modifying training dynamics—removing the Next Sentence Prediction (NSP) objective, increasing batch sizes, extending training time, and employing dynamic masking, leading to better results in downstream tasks, including NER.

Data availability, being a major driver in ML advancement, began moving toward approaches that required less labeled data. Unsupervised, weakly supervised, and few-shot learning methods gained traction by capitalizing on the representational power of pretrained language models. Self-supervised learning objectives allowed models to internalize rich syntactic and semantic information, which could then be adapted to NER with minimal supervision. These methods opened the door for expanding NER into domains and languages where annotated corpora were scarce or nonexistent.

Looking further ahead, consistent syntactic structures—particularly those captured in parse trees—are being reintegrated into neural architectures to enhance coherence and explainability. These tree-based approaches offer ways to impose hierarchical constraints that align with human linguistic intuition. When coupled with pretrained encoders and structured decoders such as CRFs or span-based classifiers, they provide a path forward for making NER models not only more accurate but also more interpretable.

## Cross-Linguistic and Low Resource NER

While most foundational work has focused on English, extending NER to low-resource and typologically diverse languages has generated new insights and challenges. In African languages, for instance, Abdulmumin and Galadanci (2019) introduced Hausa word embeddings (hauWE), developed using Continuous Bag of Words and Skip-Gram models. These embeddings far surpass fastText-based representations in downstream tasks like NER, demonstrating the need for tailored embedding models.

Ifeoluwa, Neubig, Ruder, Rijhwani, Nakatumba-Nabende, Ogundepo, and Klakow (2022) tackled the broader challenge of underrepresentation in African NLP by assembling the largest manually annotated NER dataset for 20 African languages. Their study found that zero-shot transfer performance varies greatly depending on the source language used during training. Carefully selecting this language improved average F1 scores by up to 14 points compared to using English.

Adelani et al. (2020) examined the impact of distant supervision for NER in Hausa and Yoruba, showing that even weakly labeled data can significantly improve classifier performance. Their results suggest that when combined with pretrained embeddings, such as those generated from transformer models, distant supervision can double model effectiveness in low-resource conditions.

Focusing specifically on Yoruba, Omisore (2023) developed an LSTM-based model designed to recognize both named and event entities. By using a Time Distributed Output layer, the system achieved high temporal precision, yielding an F1 score of 0.8967. This highlights the adaptability of sequence models to narrative-rich and event-driven text in low-resource settings.

In another contribution to NER involving visual input, Afeez, Ibrahim, Bolaji, and Adedayo (2024) utilized ResNet-50 for OCR-based character recognition in Nigerian languages. Their work addresses the preprocessing needs of typed image text before applying NER, enabling broader adoption in mobile-first communication contexts.

Arabic NER has also seen significant progress. Al-Smadi et al. (2020) improved on previous BiLSTM-CRF models by implementing a Pooled-GRU model. Using the WikiFANEGold dataset, their new architecture achieved a 91.2% accuracy rate, representing a 17% boost in F-measure over earlier benchmarks. 

The Urdu language presents unique challenges for NER due to the absence of orthographic cues such as capitalization. To address this, the U-MNER framework (2024) integrates both text and visual modalities. Its architecture includes Urdu-BERT embeddings, self-attention, cross-modal fusion layers, and a CRF decoder, achieving high accuracy in a low-supervision setting. Such multimodal approaches offer promising directions for improving NER in structurally challenging languages.


## The Future of NER

Future NER systems must be capable of nested and fine-grained entity detection, especially in technical and biomedical domains - a growing field specifically in depolyment of ML enabled EHR. Cross-lingual transfer will remain essential, particularly for underrepresented languages. Unsupervised and self-supervised learning methods are expected to expand the frontier of zero-resource NER.

Consistent tree-based syntactic parsing is also likely to play a larger role, especially for enforcing structured boundaries and semantic coherence. The combination of consistent syntactic trees with pretrained transformer encoders may offer both robustness and interpretability. Structured outputs, such as those used in GraphRAG and knowledge graph construction, will further integrate NER into complex downstream pipelines.

From rule-based chunking to RoBERTa, CNNs, and multimodal systems, the trajectory of NER reflects the broader arc of NLP: increasing generality, adaptability, and depth. In a world of multilingual, multi-domain, and multimodal data, NER continues to be a vital gateway for transforming raw text into actionable structure.

---

## References
* Ramshaw, L. A., & Marcus, M. P. (1995). [Text Chunking using Transformation-Based Learning](https://arxiv.org/abs/cmp-lg/9505040). *Proceedings of the Third ACL Workshop on Very Large Corpora*.
* Abdulmumin & Galadanci (2019). [hauWE: Hausa Word Embeddings](https://arxiv.org/pdf/2505.07884)
* Ifeoluwa, Neubig, Ruder, Rijhwani, Nakatumba-Nabende, Ogundepo & Klakow (2022). [NER for African Languages](https://arxiv.org/pdf/2505.07884)
* Adelani, Hedderich, Zhu, Berg & Klakow (2020). [Low-resource NER for Yoruba and Hausa](https://arxiv.org/pdf/2003.08370)
* Omisore (2023). [Event NER in Yoruba](https://arxiv.org/pdf/2505.07884)
* Al-Smadi, Al-Zboon, Jararweh & Juola (2020). [NER for Arabic using Pooled-GRU](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8993806)
* Afeez, Ibrahim, Bolaji & Adedayo (2024). [OCR-to-NER with ResNet-50 for Nigerian languages](https://ceur-ws.org/Vol-3708/paper_18.pdf)
* Urdu U-MNER (2024). [Multimodal NER in Urdu](https://arxiv.org/pdf/2505.05148)
* Bird, S., Klein, E., & Loper, E. (2009). [NLTK Book, Chapter 7: Information Extraction](https://www.nltk.org/book/ch07.html)
* IBM (2019). [NER Overview](https://www.ibm.com/think/topics/named-entity-recognition)
* ARTiBA (2024). [NER with NLTK: A Practical Guide](https://www.artiba.org/blog/named-entity-recognition-in-nltk-a-practical-guide)


