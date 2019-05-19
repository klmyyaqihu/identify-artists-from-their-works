# Identify Artists from Their Works & Image Style Transfer
There are three major sections in this project:
* Build a fine tuned network based on pre-trained network `VGG16` to classify 30 artists' paintings.
* Build a fine tuned network based on pre-trained network `fastai.vision.learner` to classify 30 artists' paintings.
* Change a painting or a photo's style to a specific airtist's painting style.

We demonstrate the project through jupyter notebook.

## Folder 1: dataset analysis
* `1_download_dataset_from_kaggle.ipynb`: it demonstrates how we download datasets from https://www.kaggle.com/ikarus777/best-artworks-of-all-time, and how we split dataset into train and test folders.
* `2_Dataset_Analysis.ipynb`: After preliminary processing of the database, we analyze the basic situation of the dataset. In this section, we will present information about 50 painters and take a loook of the artist's style and personal information.

<p align="center"><img src="https://github.com/klmyyaqihu/identify-artists-from-their-works/raw/master/figures/Wordcloud.PNG" height="50%" width="50%"> </p >

## Folder 2: classification-VGG16 (with GPU)
* `1_Vgg16_30class_untune.ipynb`: In this part, we loads all qualified data (30 classes) in VGG16 without tuning. However, there exists severe overfitting by only using the VGG16. To address overfiting, we decide to first use 3 classes train a better model. And then, we go back to 30 classes and compare the results with this untuning version.
* `2_Vgg16_3class_untune.ipynb`: In this part, we only loads 3 classes with most paintings in VGG16 and still without tuning, because we need to compare it with the other tuned versions. Though this time we only run 20 epochs, we can still see there exists overfitting.
* `3_Vgg16_3class_test1 (overfitting).ipynb`: For this part, we loads 3 classes with most paintings in VGG16 and adds several layers to test the performance. Still, run 20 epochs. However, at the end of this test1, we can still clearly see overfitting.
* `4_Vgg16_3class_test2 (best fitting).ipynb`: For this part, we still loads 3 classes with most paintings in VGG16 while adds two more layers than test1. Still, run 20 epochs. Fortunately, at the end of this test2, we got nicer loss curves which reflects no obvious overfitting.
* `5_Vgg16_3class_test3 (underfitting).ipynb`: For this part, we still loads 3 classes with most paintings in VGG16 while adds two more layers than test2. Still, run 20 epochs. However, at the end of test3, we end up to an obvious underfitting.
* `6_Vgg16_3class_test2_validation1.ipynb`: Based on all three tests' results, the test2 has the best performance. Thus, we decide to repeat the test2's model two more times which verify the modle may work well on 30 classes. This is the validation1.
* `7_Vgg16_3class_test2_validation2.ipynb`: This is the validation2 of test2.
* `8_test_3class_result_summary.ipynb`: For this part, we compare the results of all test models for 3 classes: untuned, test1, test2, and test3. We will use the `loss`, `val_loss`, `acc`, and `val_acc` from former tests. And `test2` is the best fitting.
* `9_Vgg16_30class_by_test2_model`: Finally, we use the model from test2 to classify 30 artists' paintings with 120 epochs. And the validation accuraccy is stable at more than %60, and the validation loss keep decreasing during the 120 epochs while keep reasonable difference between the training loss. Given that there are 30 classes and some of the artists have similar art style, the accuracy of 60% is an acceptable result.
* `10_30class_result_summary`: For this part, we compare the results two models for 3 classes: untuned, and the model from test2. We will use the loss, val_loss, acc, and val_acc from the former tests. From the untuned_loss_curve, the val_loss keep increasing during all 120 epoch, which reflects severe overfitting; By comparison, from the test2_loss_curve, the val_loss keep decreasing during the 120 epochs which is what we expect.
<p align="center"><img src="https://github.com/klmyyaqihu/identify-artists-from-their-works/raw/master/figures/30class_result_summary_1.png" height="95%" width="95%"> </p >
<p align="center"><img src="https://github.com/klmyyaqihu/identify-artists-from-their-works/raw/master/figures/30class_result_summary_2.png" height="48%" width="48%"> </p >

## Folder 3: classification-fastai.vision (with GPU)
* `fastai_30class_25epoch`: In this section, we try to classify the paintings of 30 artists using fastai vision. At the same time, in order to improve the accuracy, we use the following methods to enrich the data of the training set: flip, rotate, contrast adjustment. We used a confusion matrix to represent the experimental results. The final result of the experiment shows that the val-loss approximately equals to train-loss, showing that the training model has no overfitting. The accuracy of the test set reached more than 81%, which is higher than the VGG16-based model. We found that the paintings of the High Renaissance School were easy to classify. Through the display of the pictures, it was found that the genre was mostly portraits of religion and the court, and it was difficult for human experts to distinguish.
<p align="center"><img src="https://github.com/klmyyaqihu/identify-artists-from-their-works/raw/master/figures/fastai_30class_25epoch_1.png" height="48%" width="48%"> </p >
<p align="center"><img src="https://github.com/klmyyaqihu/identify-artists-from-their-works/raw/master/figures/fastai_30class_25epoch_2.png" height="48%" width="100%"> </p >

## Folder 4: image style transfer
* `image-style-change`: (This part we got inspiration and learning from https://www.kaggle.com/basu369victor/style-transfer-deep-learning-algorithm) First, we have an original image and a style image. Then, we still use VGG16 but only pick the convolution layers for extracting image's features and delete the layers for classification. Finally, we will get a new picture combine the style of the style image and the objects from original image.
* `image-style-change (another example)`: This part has the same codes with 'image-style-change' but using a different orignal image and a style image.
<p align="center"><img src="https://github.com/klmyyaqihu/identify-artists-from-their-works/raw/master/figures/image-style-change.png" height="48%" width="100%"> </p >
