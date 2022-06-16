<template>
  <img src="./assets/sheep.jpg" id="img1">
  <input type="file" @change="previewFiles">
  <div>
    Make and model: <span id="makeAndModel"></span>
  </div>
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
      EXIF.getData(event.target.files, function () {
        const make = EXIF.getTag(this, 'Make');
        const model = EXIF.getTag(this, 'Model');
        const makeAndModel = document.getElementById('makeAndModel');
        makeAndModel.innerHTML = `${make} ${model}`;
      });

      EXIF.getData(event.target.files, () => {
        const orientation = EXIF.getTag(this, 'Orientation');
        console.log(orientation);
      });
    };

    // eslint-disable-next-line no-use-before-define
    window.onload = getExif;

    function getExif() {
      const img1 = document.getElementById('img1');
      console.log(img1);
      EXIF.getData(img1, function () {
        const allTag = EXIF.getAllTags(this);
        const makeAndModel = document.getElementById('makeAndModel');
        makeAndModel.innerHTML = `${allTag}`;
        console.log(allTag);
      });
    }
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
