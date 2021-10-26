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
          v-model="message"
          label="Message"
          required
          prepend-icon="mdi-message"
          ></v-text-field>

          <v-btn
          color="primary"
          class="mr-4"
          @click="decrypt"
          >
            Decrypt
          </v-btn>

      </v-sheet>

    </v-sheet>
  </div>  
</template>

<script>
export default {
    data: () => ({
      select: null,
      valid: true,
      thumbnail1: null,
      message: "",
      url1: null
    }),

    methods: {
        getBase64(file) {
          return new Promise((resolve, reject) => {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = () => resolve(reader.result);
            reader.onerror = error => reject(error);
          });
        },
        base64ToHex(str) {
          const raw = atob(str);
          let result = '';
          for (let i = 0; i < raw.length; i++) {
            const hex = raw.charCodeAt(i).toString(16);
            result += (hex.length === 2 ? hex : '0' + hex);
          }
          return result.toUpperCase();
        },

        text2Binary(string) {
            return string.split('').map(function (char) {
                return char.charCodeAt(0).toString(2);
            }).join(' ');
        },

        middleware() {
          this.getBase64(this.thumbnail1).then(data => {
            let message = this.text2Binary(this.message);
            let s = ""
            let counter = 0
            let str = data;
            for(let i=0; i<str.length; i++) {
              if(str[i] == ",") counter++;
              else if(counter) {
                s += str[i];
              }
            }
            str = s;

            if(message.length > data.length) {
              console.log("message size is very large");
            }
            else {
              //
            }

            console.log(message)
            console.log(data);
          })
        },
        
        decrypt () {
          
          this.middleware();
          console.log("Validate");
        },

        Preview_image1() {
          if(this.thumbnail1 == null) return;
          if(this.isImage(this.thumbnail1.name) == false) {
              this.$refs.image1.reset();
              this.thumbnail1 = null;
              return;
          }
          this.url1 = URL.createObjectURL(this.thumbnail1)
        },

        getExtension(filename) {
          var parts = filename.split('.');
          return parts[parts.length - 1];
        },

        isImage(filename) {
          var ext = this.getExtension(filename);
          switch (ext.toLowerCase()) {
            case 'jpg':
            case 'jpeg':
            case 'png':
            case 'svg':
            case 'gif':
              // etc
              return true;
            }
            return false;
          }
    }
}
</script>