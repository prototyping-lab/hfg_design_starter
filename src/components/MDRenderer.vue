<template>
    <div class="mdcontainer">
      <square v-if="!isLoaded" class="spinner"></square>
      <vue-markdown v-if="isLoaded" :source="content" :linkify="false" class="mddocument"></vue-markdown>
    </div>
</template>
<script>

import VueMarkdown from 'vue-markdown';

export default {
  components: {
    VueMarkdown
  },
  name: "MDRenderer",
  props: {
    file: {
      type: String,
      default: "No content",
    }    
  },
  data () {
    return {
      content: "Lade Inhalte",
      isLoaded: false,
    }
  },
  watch: { 
   file: {
        // the callback will be called immediately after the start of the observation
        immediate: true,
        handler (newVal, oldVal) { // watch it
          this.isLoaded = false;
          this.loadFile(newVal)
        }
    }
  },
  methods: {
    loadFile: function(fileId) {
          console.log("Loading "+fileId);
          this.$gapi.request({
                path: 'https://www.googleapis.com/drive/v3/files/'+fileId,
                method: 'GET',
                params: {
                    mimeType: "text/plain",
                    alt: "media",
                }
            }).then(response => {
                this.content = response.body;
                this.isLoaded = true;
            }).catch(function (error) {
                // handle error
                console.log(error);
            })
      }
  },
  mounted() {
    this.$store.watch(
      state => state.isLoggedIn,
      () => {
        //reload after login/logout (update access rights)
        this.loadFile(this.file);
      }
    );
  }
};
</script>
<style>
  .spinner {
    display: block;
    margin:auto;
  }

  .mdcontainer {
    width:100%;
    margin-left:5%;
  }

  .mddocument img {
    max-width:100%;
  }

  .mddocument a {
    text-decoration: underline;
  }
</style>