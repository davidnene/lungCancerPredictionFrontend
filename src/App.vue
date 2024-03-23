<script setup>
  import { ref } from 'vue'
import ModelDescVue from './components/ModelDesc.vue';
</script>

<template>
  <v-layout class="rounded rounded-md">
    <v-app-bar title="ResNet50" style="color: blue;font-weight: bolder;" class="text-center"></v-app-bar>

    <!-- <v-navigation-drawer>
      <v-list>
        <v-list-item title="Navigation drawer"></v-list-item>
        
      </v-list>
    </v-navigation-drawer> -->
    <!-- <Navigation title="Navigation drawer"/> -->

    <v-main class="align-center justify-center" style="min-height: 100%;">
      <div>
        <div class="container pt-4 pb-4">
          <div class="row">
            <div class="col-md-6 col-sm-12" style=" min-height: 670px;">
              <ModelDescVue/>
            </div>
            <div class="col-md-6 col-sm-12">
              <Form/>
            </div>
          </div>
        </div>
      </div>
      
    </v-main>
  </v-layout>
</template>

<style scoped>

</style>

