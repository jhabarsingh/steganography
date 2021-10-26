<template>
  <div>
    <v-sheet
      color="white"
      elevation="3"
      style="padding:10px;width:99%;margin:auto;"
    >
      <p class="text-h4 text--primary">
        Encryption
      </p>
      
      <v-sheet 
        elevation="1"
        style="width:80%;margin:auto;padding:10px;"
      >
        <v-file-input
          label="Upload Image"
          @change="Preview_image1"
          v-model="thumbnail1"
          ref="image1"
          prepend-icon="mdi-camera"
        ></v-file-input>


        <v-img
            v-if="thumbnail1"
            :src="url1"
            style="margin:20px auto; width:400px;"
            aspect-ratio="1"
            class="grey lighten-2"
          >
          </v-img>

        <v-text-field
          v-model="cost_price"
          label="Message"
          required
          prepend-icon="mdi-message"
          ></v-text-field>

          <v-btn
          color="primary"
          class="mr-4"
          @click="validate"
          >
            Download
          </v-btn>

      </v-sheet>

    </v-sheet>
  </div>  
</template>