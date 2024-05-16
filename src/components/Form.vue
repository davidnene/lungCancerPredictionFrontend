<script setup>
import { ref, reactive } from 'vue'

 const image = ref(null);
 const base64String = ref(null);
 const imageUrl = ref(null)
 const pred = ref(false)
 const tNow = ref(null)
 const currentTimeUpdate = ref(null)
 const results = reactive({
    prediction: null,
    probability:null
 })

 const predStart = () => {
    pred.value = true
 }

 const convertToBase64 = (file) => {
    const reader = new FileReader();

    reader.onload = () => {
      base64String.value = reader.result.split(',')[1];
    };

    reader.onerror = (error) => {
      console.error('Error converting image to base64:', error);
    };

    reader.readAsDataURL(file);
  };

 function handleImageUpload(e){
    image.value = e.target.files[0]
    const imageFile = e.target.files[0]
    base64String.value = convertToBase64(image.value)
    if(imageFile) {
        imageUrl.value = URL.createObjectURL(imageFile)
    }

    
    
 }

 
 function submitImage(e){
    e.preventDefault();
    
    const sendData = {
    'cancer_image': base64String.value
 }
    fetch("https://lungcancerpredictionapi.onrender.com/predict", {
    method: "POST",
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(sendData)
  })
  .then(response => {
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    return response.json();
  })
  .then(data => {
    results.prediction = data['prediction']
    results.probability = data['probability']
  })
  .catch(error => {
    console.error("Error:", error);
    // Handle errors here
  });

  const now = new Date();
    tNow.value = now;

    const year = tNow.value.getFullYear();
    const month = tNow.value.getMonth() + 1; // Months are 0-indexed, so add 1
    const day = tNow.value.getDate();
    const hours = tNow.value.getHours();
    const minutes = tNow.value.getMinutes();
    const seconds = tNow.value.getSeconds();

    const currentTime = `${year}-${month.toString().padStart(2, '0')}-${day.toString().padStart(2, '0')} ${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    currentTimeUpdate.value = currentTime
    console.log(currentTimeUpdate.value);

    
 }

 const lungCancerData = {
  'squamous.cell.carcinoma': 'Squamous cell carcinoma of the lung arises from the squamous cells, which are flat cells lining the airways of the lung. This type of lung cancer is strongly associated with cigarette smoking, with tobacco smoke being a primary causative factor.',
  'adenocarcinoma': 'Lung adenocarcinoma is the most common subtype of non-small cell lung cancer (NSCLC) and originates in the glandular epithelial cells of the lung.',
  'large.cell.carcinoma': 'Large cell carcinoma is a type of NSCLC characterized by large, abnormal-looking cells when viewed under a microscope. This form of lung cancer is known for its rapid growth and high potential to spread to distant parts of the body.',
  'normal': 'Healthy!'
 }

</script>

<template>
  <div class="pt-6">
    <form @submit="submitImage" class="pb-5">
  <div class="mb-3">
    <label for="doctorName" class="form-label">Doctor's Name</label>
    <input type="name" class="form-control" id="doctorName" required>
  </div>
  <div class="mb-3">
    <label for="exampleInputPassword1" class="form-label">Image Upload</label>
    <input type="file" id="image" class="form-control" name="image" accept="image/*" @change="handleImageUpload" required>
  </div >
  <button type="submit" class="btn btn-warning" :onClick="predStart">Classify</button>
</form>
</div>
<div v-if="results.probability" class="card mb-3" style="max-width: 650px;">
  <div class="row g-0">
    <div class="col-md-4">
      <img :src="imageUrl" :alt="results.prediction" :title="results.prediction" class="img-fluid rounded-start">
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h5 class="card-title">Classification Results</h5>
        <p class="card-text"><b>Classification: </b> {{ results.prediction }}<br/><b>Probability:</b> {{ results.probability }}% </p>
        <p v-if="results.prediction === 'large.cell.carcinoma' || 'normal' || 'squamous.cell.carcinoma' || 'adenocarcinoma'" class="card-text">{{ lungCancerData[results.prediction] }}</p>
        <p v-if="results.probability" class="card-text"><small class="text-body-secondary">Classification Time: {{ currentTimeUpdate}}</small></p>
      </div>
    </div>
  </div>
</div>
</template>
