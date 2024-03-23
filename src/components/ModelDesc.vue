<script setup>

</script>
<template>
    <div class="text-center">
        <h3 style="color: blue;">Lung Cancer Prediction Model</h3>
        <p class="btn btn-warning" style="font-weight: bold;">Abstract</p>
    </div>
    <div>
        <div class="pb-3">
            <p class="">
                This research study developed a Convolution Neural Network (CNN) model for enhanced classification of cancer utilizing CT scan images by fine-tuning the pre-trained ResNet50 architecture. Utilizing Pytorch, a leading deep learning framework for computer vision, the model was trained on a curated dataset from the public Lung Image Database Consortium (LIDC), a medical imaging database for development, training, and evaluation of computer-assisted diagnostic (CAD) methods for lung cancer detection and diagnosis
            </p>
        </div>
        <div>
            <p class="pb-3">
                The collected CT scan image include various types of lung cancer, such as adenocarcinoma, squamous cell carcinoma, large cell carcinoma, and normal tissue. Data pre-processing techniques such as resizing, normalization, converting and data augmentation techniques were used to ensure compatibility with the pre-trained model.
            </p>
        </div>
        <div>
            <p class="pb-3">
                The model's performance was evaluated with a range of metrics, demonstrating an accuracy of 87.5%, precision of 80.97%, and an F1 score of 77.4%. These results indicate a promising capability for the model to accurately classify types of lung cancer, supporting its potential use in clinical settings.
            </p>
        </div>
        <div class="text-center">
            <p style="color: blue;">-------------------------</p>
        </div>
        <div>
            <p class="">
                <em>Author: </em>Phylis Korir<br>
                <em>Affiliation: </em> MSc. Data Science & Analytics Student<br>
                <em>Institution: </em> Strathmore University<br>
            </p>
        </div>
        <div class="text-center">
            <p style="color: blue;">-------------------------</p>
        </div>
    </div>
</template>

<style lang="scss" scoped>
 .content-color{
    color: white;
 }
</style>