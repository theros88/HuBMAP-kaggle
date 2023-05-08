# Increasing accuracy by using SegFormers
- A new notebook was created to generate a dataset in kaggle of 1024x1024 images and 
their respective masks (2 classes only: background and FTUs). This dataset will be used
with a SegFomer model.
- A Colab notebook for fine-tuning a pre-trained mit-b4 SegFormer model was created. The 
model was fine-tuned with the rescaled 1024x1024 dataset with heavy augmentations applied
and particularly the `RandomCutOut` technique proved to be very beneficial in helping improve 
the model's performance and generalization. Only two classes were used for semantic segmentation
(background and FTU mask). The final scores of this model in regard to the
Dice metric were: `mDice: 0.9322, Dice.BG: 0.9875, Dice.FTU: 0.8769`.
