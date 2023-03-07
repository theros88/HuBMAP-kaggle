# HuBMAP + HPA - Hacking the Human Body Kaggle Competition
The Human BioMolecular Atlas Program (HuBMAP) is working to create a Human Reference Atlas at the cellular level. Sponsored by the National Institutes of Health (NIH), HuBMAP and Indiana University’s Cyberinfrastructure for Network Science Center (CNS) have partnered with institutions across the globe for this endeavor. A major partner is the Human Protein Atlas (HPA), a Swedish research program aiming to map the protein expression in human cells, tissues, and organs, funded by the Knut and Alice Wallenberg Foundation.

In this competition, we had to identify and segment functional tissue units (FTUs) across five human organs. The notebooks in this project were used to build a model using a dataset of tissue section images and with the goal of segmenting FTUs as accurately as possible.

At first, a baseline was created by submitting segmentation masks which were produced randomly using a uniform distribution. This gave us a Public Score of 0.29014 accuracy (the actual metric that was used was the mean Dice coefficient).
Then, a U-Net CNN model is used based on resnet34 architecture, which is trained with optimal LR. Inference on the test dataset is performed in a seperate step and this gave a precision of 0.44730 (Public Score)

(Results and conclusiuons TO BE CONTINUED)
