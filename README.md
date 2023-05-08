# HuBMAP + HPA - Hacking the Human Body Kaggle Competition
![image](https://user-images.githubusercontent.com/103253087/236857789-62d0cf84-378b-4a2d-82da-b691c1cbd4ab.png)

The Human BioMolecular Atlas Program (HuBMAP) is working to create a Human Reference Atlas at the cellular level. Sponsored by the National Institutes of Health (NIH), HuBMAP and Indiana University’s Cyberinfrastructure for Network Science Center (CNS) have partnered with institutions across the globe for this endeavor. A major partner is the Human Protein Atlas (HPA), a Swedish research program aiming to map the protein expression in human cells, tissues, and organs, funded by the Knut and Alice Wallenberg Foundation.

In this research code competition, we had to identify and segment functional tissue units (FTUs) across five human organs. The notebooks in this project were used to build and train models using a dataset of tissue section images and with the goal of segmenting FTUs as accurately as possible. More details on the competition can be found [here](https://www.kaggle.com/competitions/hubmap-organ-segmentation/overview).

To understand more the dataset of the competition, an [Exploratory Data Analysis notebook](https://github.com/theros88/HuBMAP-kaggle/blob/main/eda-for-hubmap-hpa-competition.ipynb) has been created and it is included in this repository, with some useful preliminary remarks.   

At first, a baseline was created by submitting segmentation masks which were produced randomly using a uniform distribution. That gave us a Public Score of 0.29014 (mean Dice coefficient) and a Private Score of 0.32931.
Then, a U-Net CNN model is used based on a Resnet34 architecture, which is trained with optimal LR. No image augmentation has been performed. Inference on the test dataset is performed in a seperate step and this gave us a Public Score of 0.44730 but a Private Score of 0.34321.

## Results and further development
After this attempt, it bacame obvious that there was an improvement in the accuracy from the baseline of ~1.5x, but in the private 50% of the test dataset, only a marginal 1.042x was gained (private score inference:0.34321 vs baseline's: 0.32931), which is deemed insignificant.  
*Proposed enchancements*
- One of the main issue is the down-sizing of the high-resolution medical images to 512x512 used for training (original average size ~ 3000x3000). Above this resolution, it was impractical/unfeasible to train the *fastai* U-Net model in a reasonable amount of time. Apparently, the loss of signal in the process of down-sizing and training is considerable and an alternative model architecture could be used (e.g. SegFormer) in order to achieve decent accuracy of the model used. 
- Heavy image augmentation techniques is possible to enhance accuracy, as the training dataset is quite small (~350 images)
- An ensemble of different model architectures should be further used to improve the accuracy. 
- Out Of Fold predictions may also enhance the generalization of the model(s)
- As all the test image datasets are from a different source than the training dataset, external image files should be merged into the training dataset

## Actions taken so far
- A resized dataset of 1024x1024 resolution was created and a SegFormer mit-b4 pre-trained model was fine-tuned on the resized dataset. Indeed, the new architecture could easily be trained on larger images with only a fraction of the resources (both memory and training time) required by a U-Net CNN architecture. Heavy augmentations were also used during training the model. In inference, different thresholds were used to identify the FTUs' masks depending on the organ category of the image. This approach resulted in a mean Dice Public Score of 0.57659 and a Private Score of 0.50252 in the test datasets of the competition. A significant improvement compared to the U-Net architecture, especially for the private score. All these can be seen in the [SegFormer](https://github.com/theros88/HuBMAP-kaggle/tree/main/SegFormer) folder in detail.
