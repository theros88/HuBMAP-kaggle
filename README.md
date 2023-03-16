# HuBMAP + HPA - Hacking the Human Body Kaggle Competition
The Human BioMolecular Atlas Program (HuBMAP) is working to create a Human Reference Atlas at the cellular level. Sponsored by the National Institutes of Health (NIH), HuBMAP and Indiana University’s Cyberinfrastructure for Network Science Center (CNS) have partnered with institutions across the globe for this endeavor. A major partner is the Human Protein Atlas (HPA), a Swedish research program aiming to map the protein expression in human cells, tissues, and organs, funded by the Knut and Alice Wallenberg Foundation.

In this competition, we had to identify and segment functional tissue units (FTUs) across five human organs. The notebooks in this project were used to build model(s) using a dataset of tissue section images and with the goal of segmenting FTUs as accurately as possible.  

For more detailed information on the datasets of the competition, an Exploratory Data Analysis notebook has been created and is included in this repository, with some useful preliminary remarks.  

At first, a baseline was created by submitting segmentation masks which were produced randomly using a uniform distribution. This gave us a Public Score of 0.29014 accuracy (the actual metric that was used was the mean Dice coefficient).
Then, a U-Net CNN model is used based on a Resnet34 architecture, which is trained with optimal LR. No image augmentation has been performed. Inference on the test dataset is performed in a seperate step and this gave a precision of 0.44730 (Public Score).

## Results and further development
After this attempt, it bacame obvious that there was an improvement in the accuracy from the baseline of ~1.5x, but in the private 50% of the test set only a marginal 1.042x was gained (private score inference:0.34321 vs baseline's: 0.32931), which is deemed insignificant.  
*Proposed enchancements*
- One of the main issue is the down-sizing of the high-resolution medical images to 512x512 used for training (original average size ~ 3000x3000). Above this resolution, it was impractical/unfeasible to train the *fastai* U-Net model in a reasonable amount of time. Apparently, the loss of signal in the process of down-sizing and training is considerable and an alternative model architecture could be used (e.g. SegFormer) in order to achieve decent accuracy of the model used. 
- An ensemble of different model architectures should be further used to improve the accuracy. 
- Out Of Fold predictions may also enhance the generalization of the model(s)
- As all the testset images are from a different source than the training dataset, external image files should be merged into the training dataset
- Heavy image augmentation techniques is possible to enhance accuracy, as the training dataset is quite small (~350 images) 
