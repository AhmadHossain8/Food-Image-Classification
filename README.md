# Food Image Classification Using Parameter Averaging and Model Ensembling

Food is essential for our lives. With the onset of the internet, thousands of food photos are shared daily on social media platforms worldwide. From individuals posting photos of their meals to food bloggers and critics sharing images on their websites and social media, food images make up a vast portion of the media found on the internet.

Correct classification of food images is essential for advertisers looking to target their content based on individual preferences. Incorrect classification results in advertisers missing their target audience, and health-conscious people may fail to check important details like calorie intake and ingredients. 

Nowadays, AI and image recognition are making it easier to classify food images accurately. In this project, we experimented with various techniques to improve the accuracy of food image classification using limited resources.

## Experiment Overview

We tested two main techniques:
1. **Parameter Averaging**: Averaging the parameters of trained models to increase accuracy.
2. **Model Ensembling**: Combining multiple models to improve classification accuracy.

In our experiment, we trained **74 models** and created **15 different combinations**. Results showed:

- Averaging parameters improved accuracy in 75% of models.
- 11 out of 15 model combinations had improved accuracy with model ensembling and parameter averaging (73.33% improvement).
- The highest accuracy (95.24%) was achieved using an ensemble of **InceptionV3**, **ResNet50**, and **VGG16** with average parameter and model ensembling techniques.

## Dataset

The dataset used for this experiment is available on Kaggle: [Food11 Dataset](https://www.kaggle.com/datasets/vermaavi/food11).

## Results

## Model Performance Table

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
| InceptionV3, Resnet50, VGG16           | 93.75             | 94.23            | 94.44                     | 94.65                    | 94.92                | 95.24                         |
| Alexnet, InceptionV3, Resnet50, VGG16  | 94.35             | 94.17            | 94.17                     | 94.83                    | 94.17                | 95.15                         |



### Key Findings:
- **Parameter Averaging** increased accuracy in 75% of models.
- **Model Ensembling** with parameter averaging showed improvement in 73.33% of combinations.

## Conclusion

We found that both parameter averaging and model ensembling significantly enhanced the accuracy of food image classification. The combination of **InceptionV3**, **ResNet50**, and **VGG16** using the average ensemble technique yielded the best performance, with an accuracy of **95.24%**.

## How to Run

Clone this repository:
    ```
    git clone https://github.com/AhmadHossain8/Food-Image-Classification.git
    ```


Download the dataset from [Kaggle](https://www.kaggle.com/datasets/vermaavi/food11).

