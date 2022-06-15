<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <input type="file" @change="previewFiles">
</template>

<script>
import EXIF from 'exif-js';

export default {
  name: 'App',
  components: {
  },
  setup() {
    const previewFiles = (event) => {
      console.log(event.target.files);

      EXIF.getData(event.target.files, () => {
        const make = EXIF.getTag(this, 'Make');
        const model = EXIF.getTag(this, 'Model');
        console.log(make);
        console.log(model);
      });

      EXIF.getData(event.target.files, () => {
        const orientation = EXIF.getTag(this, 'Orientation');
        console.log(orientation);
      });
    };

    return {
      previewFiles,
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
