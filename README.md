# Capstone-Overview
Welcome to the Language of Proteins, Capstone Repo for Fourth Brain MLE 10; by Dr Shaista Hussain, Mr Jonathan Grant &amp; Dr Anjana Sengupta

* DEPLOYED MODEL [Hugging Face]*
https://huggingface.co/spaces/jonathang/Protein-Family-Ensemble

* PRESENTATION *
https://docs.google.com/presentation/d/1Y4d-p-nfWR-acm4jbape_KBqOIE6aOSZkYMbguDYNVY/edit?usp=sharing


We aimed to apply NLP to amino acid sequences to predict if we could classify them into protein families (originally into Anticancer Peptides (ACPs), DNA-Binding proteins (DBPs), Antimicrobial peptides (AMPs); later decided to use 1000 protein families.

* Iterations* 
We realized that the datasets provided limited us to just 3 protein family categories, and we aspired to reach for a greater number of family detection with a larger dataset.  Therefore, we opted to use the PFAM dataset, a protein family database with annotations and sequence alignments, represented by HMMs - automatically built from seed alignment and searched against the hmmer.org sequence database.  We split the data into train 80, val 10, test 10%, and ran several baselines (https://colab.research.google.com/drive/1UdB8tBaKF9YaV_Vz_v3MBvNG0CfWpfrS?usp=sharing, https://colab.research.google.com/drive/1xEplFlL29t5hWjldvP48ZAnNaj8gr64M?usp=sharing, https://colab.research.google.com/drive/1KC1jFXByjyN6YF1zJ8f0xCyVuGHX6F_k?usp=sharing, https://colab.research.google.com/drive/1mlCJuH6rVh8dsOIobHNlLKArOoP-o6W1?usp=sharing, https://colab.research.google.com/drive/13qKCmrU0tQkL_5nDhKPMzMnnpoAfPONj#scrollTo=uPZiBF6ca_Sh:~:text=https%3A//www.kaggle.com/code/luckyapollo/pfam%2Dproteinprediction, https://colab.research.google.com/drive/1uZ3VDsMRcxvfLi-ldQczT1PdqmoHWHxy?usp=sharing, https://colab.research.google.com/drive/1UdB8tBaKF9YaV_Vz_v3MBvNG0CfWpfrS?usp=sharing, https://colab.research.google.com/drive/1fiQNvhN6wtqOCB3PMyrZIYRvRyl9kQqm?usp=sharing, https://www.kaggle.com/luckyapollo/protein-sequence-family, https://www.kaggle.com/code/luckyapollo/predicting-protein-classification, 
then
https://gist.github.com/JonathanGrant/c3722e90197889d4a5e0d98af2a47402#file-protein_pfam_protbert_xgboost_1000-ipynb, https://gist.github.com/JonathanGrant/759304e8935dbdcf5ad4ebe7687f720a, https://colab.research.google.com/github/TheLastBen/fast-stable-diffusion/blob/main/fast-DreamBooth.ipynb#scrollTo=iAZGngFcI8hq and https://colab.research.google.com/gist/JonathanGrant/59c9f49a75aa5c74260888e0dd5a75c5/protein_pfam_hierarchical_1.ipynb, and https://colab.research.google.com/gist/JonathanGrant/59c9f49a75aa5c74260888e0dd5a75c5/protein_pfam_hierarchical_1.ipynb  until we arrived at the baseline https://colab.research.google.com/drive/1OoZozgiLb-j7xFM3VoknPbglemXe__8l?usp=sharing .

Delivery format: via Hugging Face https://huggingface.co/spaces/jonathang/Protein-Family-CNN 
Starting out, we used GPUs & High-Ram on Colab Pro. Later, we used Kaggle and Lambda Labs with high memory & CPU. From the simplest to complex models, memory and speed were our major limitations.
Solutions to limitations: iFeatures for reads AA sequence; HuggingFace
Should the model be deployed to run in batch, or from an api or a streaming process> ran 1000 classes
What sort of infrastructure will be required for training? Transfer learning - doesn’t require many resources: 1 x GPU with Google CoLab/person

Our initial model used XGBoost to classify the proteins into 1000 classes. The weighted averages are fairly low - [1] Precision = 0.70 [2] Recall = 0.69 [3] F1-score = 0.69.

Next we tried LSTM: 25 epochs and achieved a higher Precision: 0.86, Recall: 0.86 F1-Score: 0.86; 

Next we tried Transformer (ProtBert Embeddings): Lambda Labs, 30 cpu, 24GB mem, batch size 2**6. Each epoch ~ 40 mins, 11 epochs, achieving: Precision: 0.94, Recall: 0.94, F1-Score: 0.94. 
 
Finally, we tried PROT CNN, 1000 classes, 3 epochs and amazingly achieved: Precision: 0.99, Recall: 0.99, F1-Score: 0.99 https://colab.research.google.com/drive/13qKCmrU0tQkL_5nDhKPMzMnnpoAfPONj?usp=sharing

* References * 

GoFair (2022). FAIR Principles https://www.go-fair.org/fair-principles/ 

Jumper, J., Evans, R., Pritzel, A. et al. Highly accurate protein structure prediction with AlphaFold. Nature 596, 583–589 (2021). https://doi.org/10.1038/s41586-021-03819-2

Roshni KG (2021) Protein folding, misfolding, and coping mechanism of cells–A short discussion. Open J Cell Protein Sci 4(1): 001-004. DOI: 10.17352/ojcps.000003

Ofer, D., Brandes, N., and Linial, M. Language of Proteins: NLP, machine learning, and protein sequences. Computational and Structural Biotechnology Journal (2021).

Bepler, T. and Berger B. Learning the Protein Language: Evolution, Structure, and Function. Cell Systems (2021).

Villegas-Morcillo, A., Gomez, A., Victoria Sanchez. An Analysis of Protein Language Models Embeddings for Fold Prediction. BioRxiv (2022).

Grechishnikova, D. Transformer neural network for protein-specific de novo drug generation as a machine translation problem. Sci Rep 11, 321 (2021). 

Ponomarenko EA, Poverennaya EV, Ilgisonis EV, Pyatnitskiy MA, Kopylov AT, Zgoda VG, Lisitsa AV, Archakov AI. The Size of the Human Proteome: The Width and Depth. Int J Anal Chem. (2016).

Antonina Andreeva, Dave Howorth, Cyrus Chothia, Eugene Kulesha, Alexey Murzin, SCOP2 prototype: a new approach to protein structure mining. (2014) Nucl. Acid Res., 42 (D1): D310-D314 and Antonina Andreeva, Eugene Kulesha, Julian Gough, Alexey Murzin, The SCOP database in 2020: expanded classification of representative family and superfamily domains of known protein structures. (2020) Nucl. Acid Res., 48 (D1): D376-D382


