<template>
  <div class="project">
    <h3>Create a new project</h3>
    <div class="project__container">
      <div class="project__item">
        <label for="title">Title</label>
        <input v-model="project.title" name="title" type="text" />
      </div>
      <div class="project__item">
        <label for="body">Body</label>
        <textarea v-model="project.body" name="body" type="textField" />
      </div>
      <div class="project__item">
        <label for="slogan">Slogan</label>
        <input v-model="project.slogan" name="slogan" type="text" />
      </div>
      <div class="project__item">
        <label for="desktop">Desktop Image URL</label>
        <input v-model="project.desktopImageUrl" name="desktop" type="text" />
      </div>
      <div class="project__item">
        <label for="tablet">Tablet Image URL</label>
        <input v-model="project.tabletImageUrl" name="tablet" type="text" />
      </div>
      <div class="project__item">
        <label for="mobile">Mobile Image URL</label>
        <input v-model="project.mobileImageUrl" name="mobile" type="text" />
      </div>
      <div class="project__item">
        <label for="link">Website URL</label>
        <input name="link" type="text" />
      </div>
      <div class="project__item">
        <label for="more">More Information</label>
        <textarea name="more" type="textField" />
      </div>
      <Btn text="Save Project" @click="checkForm" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import * as config from "../../../config";
import Btn from "../button/Btn";
export default {
  name: "adminProject",
  components: {
    Btn
  },
  data: function() {
    return {
      project: {
        title: '',
        slogan: '',
        body: '',
        url: '',
        desktopImageUrl: '',
        tabletImageUrl: '',
        mobileImageUrl: '',
      }
    };
  },
  methods: {
    createProject: function() {
      return axios
        .post(`${config.apiUrl}/projects`, this.project)
        .then(() => {
          this.$router.push({ path: "/admin" });
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    checkForm: function(evt) {
      evt.preventDefault();
      this.errors = [];
      if (!this.project.title) {
        this.errors.push("Title required");
      }
      if (!this.project.body) {
        this.errors.push("Body required");
      }
      if (!this.project.url) {
        this.errors.push("Link required");
      }
      this.createProject();
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../../assets/scss/_variables";

.project {
  padding: 2rem 6rem;
  width: 100vw;

  &__container {
    width: 100%;
    columns: 2;
    column-gap: 5rem;
  }
  input {
    padding: 0.5rem;
    width: 100%;
  }
  textarea {
    width: 100%;
    resize: none;
    min-height: 10rem;
  }
  &__item {
    padding: 0.5rem 0;
  }
}
</style>