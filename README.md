# TCRBinder: Pathogen-recognition prediction in the Human Immune System

## Introduction
The human adaptive immune system's ability to recognize and eliminate pathogens and malignant cells is a cornerstone of health. This function is primarily mediated by T-cells, which utilize a highly specific receptor (TCR). T-cells inspect small protein fragments ( epitopes) that are "presented" to them on the surface of other cells. The incredible diversity of the TCR repertoire allows the immune system to respond to a vast number of potential threats. However, this same diversity presents a challenge: predicting which T-cell will recognize which epitope.
Solving this "specificity" problem is a central goal in computational immunology. This project confronts this challenge by developing a deep learning classifier to predict if a given (TCR, Epitope) pair will interact, leveraging the power of Convolutional Neural Networks (CNNs) to learn generalizable sequence patterns from the paired data that determine a "Yes/No" binding event.

## Background & Motivation
A functional TCR is a heterodimer, composed of two distinct chains, an alpha (TRA) chain and a beta (TRB) chain, which pair together to form the antigen-binding site. The beta chain contains the highly diverse CDR3 loop, which is widely considered the primary determinant of specificity and is the most common chain profiled in public databases. Therefore, this project will focus exclusively on CDR3 sequences from TCR beta for all analyses.
The combinatorial space of possible CDR3 sequences is astronomical (>1015), making an exhaustive experimental mapping of all TCR-epitope pairs impossible. Experimental methods for determining TCR specificity are low-throughput, expensive, and very labor-intensive. The recent advancement of high-throughput sequencing has led to the creation of large public databases, such as VDJdb, which pair TCR sequences with their known epitope targets. This data explosion provides the necessary fuel for data-driven, machine learning approaches to tackle this problem.
The development of a computational solution can directly impact multiple areas, such as cancer, infectious diseases and autoimmunity. This would help improve diagnostics, prognostics, and foster vaccine development.

## Data Pre-processing
To prepare the VDJdb dataset for our classification task. The initial step was to retain only records corresponding to human (Homo sapiens) TRBs, as this represents the most common and well-annotated use case in immunoinformatics. Subsequently, the dataset was reduced to only the essential columns for this study: the CDR3 amino acid sequence, serving as the predictive feature, and the Epitope, serving as the target label. Given the fact that a given antigen can be recognized by multiple combinations of TCRs, a minimum support threshold was applied, retaining only those epitopes with at least 50 associated TCR examples. We want our model to learn generalizable patterns in such sequences, and be able to predict whether there is binding between a given TCR-Epitope pair.

# Video

(link)[]

## Study Limitations

While this project establishes a strong baseline, it is crucial to acknowledge its limitations, which also serve as clear directions for future work.

The model's performance is fundamentally constrained by the available public data. VDJdb, while extensive, is limited to the CDR3 of the TCR beta-chain, neglecting the contributions of the alpha-chain and other CDR loops (CDR1, CDR2), which also influence binding. Furthermore, there is a lack of experimentally-verified negative (non-binding) pairs. Our approach has known limitations, such as the possibility of generating a pair with undiscovered cross-reactivity, and thus should be considered a plausible but not experimentally-verified negative set.

The choice of a simple CNN, while effective, does not capture long-range dependencies within the sequence as explicitly as architectures like Recurrent Neural Networks (RNNs) or Transformers might. Additionally, the use of one-hot encoding treats each amino acid as an independent entity, ignoring the underlying biochemical similarities between them. More sophisticated embeddings could provide richer input to the model.

The most significant limitation is that our model is HLA-agnostic. In reality, TCR binding is HLA-restricted, meaning a TCR recognizes an epitope only when presented by a specific HLA molecule. By ignoring the HLA context, our model learns a generalized representation of binding that may not hold true for all genetic backgrounds. Incorporating HLA information is a critical next step for developing a clinically relevant tool.

## Discussion
Here is how I would structure your "Discussion" and "Conclusion" section to tie all this together.

"This project successfully demonstrated the development and validation of a Convolutional Neural Network for the generalizable, pair-wise prediction of TCR-epitope binding. On of the model's strengths is the flexible binary classification that is not constrained to a fixed set of known antigens.

The model achieved a strong predictive performance on a held-out test set, with an Area Under the ROC Curve (AUROC) of 0.97. This indicates a high degree of separability between the positive (VDJdb-derived) and synthetic negative (shuffled) data pairs.

However, the model's true utility was demonstrated not in its accuracy, but in its interpretability. By employing in silico mutagenesis, we were able to probe the trained model to identify residue-level "hotspots" critical for binding. However, the limitations of this proof-of-concept are significant and define clear paths for future work. 

In conclusion, this project serves as a robust framework for in silico TCR specificity prediction. The combination of a CNN architecture with the mutation exercise that provides a powerful tool for discovering the sequence-level rules of immune recognition. Future iterations incorporating multi-chain and MHC-specific data, built upon this foundation, hold the potential to accelerate personalized immunotherapy and vaccine development.

## References
* Shugay, M., Bagaev, D. V., Zvyagin, I. V., Vroomans, R. M., Crawford, J. C., Dolton, G., ... & Chudakov, D. M. (2018). VDJdb: a curated database of T-cell receptor sequences with known antigen specificity. Nucleic acids research, 46(D1), D419-D427.
* Alipanahi, B., Delong, A., Weirauch, M. T., & Frey, B. J. (2015). Predicting the sequence specificities of DNA-and RNA-binding proteins by deep learning. Nature biotechnology, 33(8), 831-838.
* Rudolph, M. G., Stanfield, R. L., & Wilson, I. A. (2006). How TCRs bind MHCs, peptides, and coreceptors. Annu. Rev. Immunol., 24(1), 419-466.
* Jurtz, V. I., Jessen, L. E., Bentzen, A. K., Jespersen, M. C., Mahajan, S., Vita, R., ... & Nielsen, M. (2018). NetTCR: sequence-based prediction of TCR binding



