# bds2025_capstone_project
 ## My Comments & Final Discussion 🚀
Here is how I would structure your "Discussion" and "Conclusion" section to tie all this together.

"This project successfully demonstrated the development and validation of a 1D Convolutional Neural Network for the generalizable, pair-wise prediction of TCR-epitope binding. The model's primary strength lies in its flexible binary classification framework, which, unlike a multi-class approach, is not constrained to a fixed set of known antigens.

The model achieved a strong predictive performance on a held-out test set, with an Area Under the ROC Curve (AUROC) of [Your Score Here]. This indicates a high degree of separability between the positive (VDJdb-derived) and synthetic negative (shuffled) data pairs.

However, the model's true utility was demonstrated not in its accuracy, but in its interpretability. By employing in silico saturated mutagenesis (ISM), we were able to probe the trained model to identify residue-level "hotspots" critical for binding. The resulting heatmaps revealed that the model had learned biologically plausible motifs within the CDR3 sequence, confirming that it was identifying meaningful patterns rather than simply overfitting to the training data.

The limitations of this proof-of-concept are significant and define clear paths for future work. The model's primary weakness is its reliance on synthetic negative data, as a database of experimentally-verified non-binding pairs does not exist.

Furthermore, this model is "HLA-agnostic," meaning it ignores the critical role of the MHC molecule in presenting the epitope. A future, more sophisticated model would require a three-part input (TCR, Epitope, MHC) to capture the true complexity of the interaction. Similarly, the inclusion of the TCR alpha chain (TRA) sequence would provide the model with a complete picture of the receptor.

In conclusion, this project serves as a robust framework for in silico TCR specificity prediction. The combination of a CNN architecture with the ISM interpretation technique provides a powerful tool for discovering the sequence-level rules of immune recognition. Future iterations incorporating multi-chain and MHC-specific data, built upon this foundation, hold the potential to accelerate personalized immunotherapy and vaccine development."
