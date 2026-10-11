# Food Image Classification Using Parameter Averaging and Model Ensembling

📄 **[Read the full report (PDF)](Effects_of_Parameter_Averaging_and_Model_Ensembling_on_the_Accuracy_of_Food_Image_Classification.pdf)**: *Effects of Parameter Averaging and Model Ensembling on the Accuracy of Food Image Classification*

**Authors:** Mahiv Khan Wasi, Sibghat Ullah Rayyan Shaikh, Ahmad Hossain, Rashidul Hassan Borshon (North South University)

Food is essential for our lives. With the onset of the internet, thousands of food photos are shared daily on social media platforms worldwide. From individuals posting photos of their meals to food bloggers and critics sharing images on their websites and social media, food images make up a vast portion of the media found on the internet.

Correct classification of food images is essential for advertisers looking to target their content based on individual preferences. Incorrect classification results in advertisers missing their target audience, and health-conscious people may fail to check important details like calorie intake and ingredients.

Nowadays, AI and image recognition are making it easier to classify food images accurately. In this project, we experimented with various techniques to improve the accuracy of food image classification using limited resources.

## Experiment Overview

We tested two main techniques on four pre-trained CNNs (**AlexNet**, **VGG16**, **ResNet50** and **InceptionV3**):

1. **Parameter Averaging**: First, train a model normally and keep the best checkpoint. Then keep training it, and after each epoch replace its weights with the average of the new weights and the previous best weights. The model learns new features without forgetting the ones it already had.
2. **Model Ensembling**: Combine every possible group of the four models (11 combinations of 2, 3 or 4 models), either by averaging their outputs (traditional ensemble) or by joining their outputs and passing them through a trained fully connected layer.

We ran **74 experiments** over **15 model configurations** (the 4 single models plus the 11 ensembles). Results:

- Parameter averaging improved accuracy in 75% (3 of 4) of the single models.
- 11 of the 15 configurations were more accurate with parameter averaging (73.33%).
- The highest accuracy (**95.24%**) came from a **Traditional Average Ensemble** of **InceptionV3**, **ResNet50** and **VGG16**, which averages the outputs of models that were trained with parameter averaging.

## Dataset

We used the [Food-11 dataset](https://www.kaggle.com/datasets/vermaavi/food11) from Kaggle. It has 16,643 images in 11 classes: Bread, Dairy product, Dessert, Egg, Fried food, Meat, Noodles/Pasta, Rice, Seafood, Soup and Vegetable/Fruit.

We cut the validation set down to 991 images (about 90 per class) and moved the rest into the training set. The final splits are 12,305 training images, 991 validation images and 3,347 evaluation images.

## Setup

- **Platform:** Google Colab (NVIDIA Tesla K80 GPU, 12 GB RAM)
- **Optimizer:** SGD, learning rate 0.001, cross-entropy loss
- **Preprocessing:** images resized to 227×227 (AlexNet, VGG16, ResNet50) or 299×299 (InceptionV3), random horizontal flips, and normalization with mean 0.5 and std 0.5
- **Training:** each single model was first trained normally, then for the same number of epochs again with parameter averaging. Each ensemble was trained for 10 epochs, with parameter averaging applied in the last 5 where it was used.

## Results

### Single Models (evaluation accuracy, %)

| Model       | Normal Training | Parameter Averaging |
|-------------|-----------------|---------------------|
| AlexNet     | 86.58           | 87.09               |
| InceptionV3 | 93.99           | 94.29               |
| ResNet50    | 94.89           | 94.71               |
| VGG16       | 92.08           | 93.48               |

### Ensembles (evaluation accuracy, %)

| Model Combination                     | Baseline Ensemble | Average Ensemble | Baseline Ensemble Average | Average Ensemble Average | Traditional Ensemble | Traditional Average Ensemble |
|----------------------------------------|-------------------|------------------|---------------------------|--------------------------|----------------------|-------------------------------|
| Alexnet, InceptionV3                   | 93.51             | 93.99            | 93.66                     | 94.08                    | 93.51                | 93.49                         |
| Alexnet, Resnet50                      | 93.21             | 93.87            | 93.93                     | 94.02                    | 93.51                | 93.63                         |
| InceptionV3, Resnet50                  | 94.95             | 94.65            | 94.98                     | 94.32                    | 95.10                | 95.21                         |
| Alexnet, InceptionV3, Resnet50         | 95.01             | 94.14            | 94.26                     | 94.65                    | 93.78                | 94.80                         |
| Alexnet, VGG16                         | 92.20             | 90.88            | 91.60                     | 91.60                    | 93.36                | 93.60                         |
| InceptionV3, VGG16                     | 93.15             | 93.63            | 94.44                     | 94.56                    | 94.80                | 94.68                         |
| Alexnet, InceptionV3, VGG16            | 93.18             | 94.05            | 92.85                     | 92.85                    | 94.20                | 94.68                         |
| Resnet50, VGG16                        | 93.75             | 93.45            | 93.69                     | 93.60                    | 95.01                | 94.95                         |
| Alexnet, Resnet50, VGG16               | 93.51             | 94.08            | 93.96                     | 93.69                    | 93.69                | 94.74                         |
| InceptionV3, Resnet50, VGG16           | 93.75             | 94.23            | 94.44                     | 94.65                    | 94.92                | **95.24**                     |
| Alexnet, InceptionV3, Resnet50, VGG16  | 94.35             | 94.17            | 94.17                     | 94.83                    | 94.17                | 95.15                         |

**What the column names mean:**

- **Baseline Ensemble**: joins the outputs of the normally trained models and passes them through a trained fully connected layer.
- **Average Ensemble**: the same as Baseline Ensemble, but built from the models trained with parameter averaging.
- **… Ensemble Average**: the same ensemble, with parameter averaging also applied to the ensemble itself during its training.
- **Traditional Ensemble**: averages the outputs of the normally trained models.
- **Traditional Average Ensemble**: averages the outputs of the models trained with parameter averaging.

### Key Findings

- **Parameter averaging** raised accuracy for AlexNet, InceptionV3 and VGG16. ResNet50 dropped slightly.
- **Ensembling with parameter averaging** beat the version without it in 6 of 11 combinations for the Baseline ensembles, 8 of 11 for the Average ensembles and 8 of 11 for the Traditional ensembles.
- The best result was **95.24%** on the evaluation set (94.75% on the validation set).

## Conclusion

Parameter averaging and model ensembling both improved food image classification accuracy in most of our experiments. The best result, **95.24%**, came from the Traditional Average Ensemble of **InceptionV3**, **ResNet50** and **VGG16**. Next, we want to repeat these experiments on a more balanced dataset and try more CNN models and new averaging techniques.

See the [full report](Effects_of_Parameter_Averaging_and_Model_Ensembling_on_the_Accuracy_of_Food_Image_Classification.pdf) for the method, the architecture details and the related work.

## Repository Structure

| File | Description |
|------|-------------|
| `Alexnet_Normal_Training_With_Parameter_Averaging.ipynb` | AlexNet: normal training and parameter averaging |
| `VGG16_Normal_Training_With_Parameter_Averaging.ipynb` | VGG16: normal training and parameter averaging |
| `Resnet50_Normal_Training_With_Parameter_Averaging.ipynb` | ResNet50: normal training and parameter averaging |
| `Inception_V3_Normal_Training_With_Parameter_Averaging.ipynb` | InceptionV3: normal training and parameter averaging |
| `2_model_Combination.ipynb` | Ensembles of 2 models |
| `3_model_Combination.ipynb` | Ensembles of 3 models |
| `4_model_Combination.ipynb` | Ensemble of all 4 models |
| `Effects_of_Parameter_Averaging_and_Model_Ensembling_on_the_Accuracy_of_Food_Image_Classification.pdf` | Final project report |

## How to Run

1. Clone this repository:

   ```bash
   git clone https://github.com/AhmadHossain8/Food-Image-Classification.git
   ```

2. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/vermaavi/food11).
3. Open the notebooks in Google Colab (or Jupyter with a GPU) and update the dataset paths.
4. Run the single-model notebooks first to produce the normal and parameter-averaged weights. Then run the 2-, 3- and 4-model combination notebooks.
