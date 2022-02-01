<template>
  <div class="anim-list-root">
    <div class="button-row">
    <!-- Anim Buttons -->
      <div
        class="action-container"
        v-for="(value, index) in [1, 2, 3, 4, 5, 6]"
        :key="index"
      >
        <div class="button-container">
          <button
            :disabled="isUploading || isDownloading"
            @click="onClick(value)"
            :class="{
              button: true,
              'is-large': true,
              'is-primary': !(errors[value - 1].length > 0),
              error: errors[value - 1].length > 0,
              'is-danger': errors[value - 1].length > 0,
            }"
          >
            {{ value }}
          </button>
        </div>
      </div>
    </div>
    <div class="button-row">
      <!-- Upload Button -->
      <div class="action-container upload">
        <button
          :disabled="isUploading || isDownloading"
          :class="{
            button: true,
            'is-large': true,
            'is-success': true,
            'is-loading': isUploading,
            'is-outlined': true,
          }"
          @click="upload"
        >
          <p>Upload</p>
          <span class="icon is-large">
            <i class="mdi mdi-36px mdi-upload"></i>
          </span>
        </button>
      </div>
      <!-- Download Button -->
      <div class="action-container download">
        <button
          :disabled="isUploading || isDownloading"
          :class="{
            button: true,
            'is-large': true,
            'is-info': true,
            'is-outlined': true,
            'is-loading': isDownloading,
          }"
          @click="download"
        >
          <p>Download</p>
          <span class="icon is-large">
            <i class="mdi mdi-36px mdi-download"></i>
          </span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isUploading: {
      type: Boolean,
    },
    isDownloading: {
      type: Boolean,
    },
    errors: {
      type: Array,
    },
  },
  emits: ["modalOpen", "upload", "download"],
  setup(props, { emit }) {
    const upload = () => {
      emit("upload");
    };

    const onClick = (index) => {
      emit("modalOpen", index);
    };

    const download = () => {
      emit("download");
    };

    return { onClick, upload, download };
  },
};
</script>

<style scoped lang="scss">
@import "../assets/sass/main.scss";
.anim-list-root {
  width: 50%;
  height: 100%;
  min-height: 300px;
  display: grid;
  grid-template-rows: 2fr 1fr;
}
.action-container {
  display: grid;
  place-items: center;
}
.button-row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.upload {
  grid-row: 3;
  grid-column: 1;
}

.download {
  grid-row: 1;
  grid-column: 1;
}
</style>