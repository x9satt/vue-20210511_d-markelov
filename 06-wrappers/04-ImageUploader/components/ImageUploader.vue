<template>
  <div class="image-uploader">
    <label
      class="image-uploader__preview"
      :class="{ 'image-uploader__preview-loading': loading }"
      :style="bgImage"
      :disabled="loading"
      @click="resetImg"
    >
      <span>{{ status }}</span>
      <input
        ref="input"
        type="file"
        accept="image/*"
        class="form-control-file"
        :disabled="loading"
        @change="changeImg"
      />
    </label>
  </div>
</template>

<script>
import { ImageService } from '../ImageService';

export default {
  name: 'ImageUploader',

  model: {
    prop: 'imageId',
    event: 'change',
  },

  props: {
    imageId: {
      type: Number,
      default: null,
    },
  },

  data() {
    return {
      loading: false,
    };
  },

  computed: {
    status() {
      return this.loading ? 'Загрузка...' : this.imageId ? 'Удалить изображение' : 'Загрузить изображение';
    },

    bgImage() {
      return this.imageId ? `--bg-image: url('${ImageService.getImageURL(this.imageId)}')` : null;
    },
  },

  methods: {
    resetImg(e) {
      if (this.imageId) {
        e.preventDefault();
        this.$emit('change', null);
        this.$refs.input.value = null;
      }
    },

    async changeImg() {
      const file = this.$refs.input.files[0];
      this.loading = true;
      this.$emit('change', await this.uploadImg(file));
      this.loading = false;
    },

    async uploadImg(file) {
      const res = await ImageService.uploadImage(file);
      return res.id;
    },
  },
};
</script>

<style scoped>
.image-uploader .form-control-file {
  opacity: 0;
  height: 0;
}

.image-uploader .image-uploader__preview {
  --bg-image: var(--default-cover);
  background-size: cover;
  background-position: center;
  background-image: linear-gradient(0deg, rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), var(--bg-image);
  border: 2px solid var(--blue-light);
  border-radius: 8px;
  transition: 0.2s border-color;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 512px;
  height: 228px;
}

.image-uploader .image-uploader__preview > span {
  color: var(--white);
  font-family: 'Nunito', sans-serif;
  font-weight: 600;
  font-size: 20px;
  line-height: 28px;
}

.image-uploader .image-uploader__preview:hover {
  border-color: var(--blue);
}

.image-uploader .image-uploader__preview.image-uploader__preview-loading {
  cursor: no-drop;
}
</style>
