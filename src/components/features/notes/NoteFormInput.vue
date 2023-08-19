<template>
  <div class="row justify-content-start g-2 py-5">
    <div class="col">
      <div class="card rounded-3">
        <div class="card-body">
          <div class="card-title text-start text-capitalalize fst-normal fs-4">
            Tambah Catatan Baru
          </div>
          <hr class="text-secondary" />
          <form @submit.prevent="onSubmitHandler">
            <div class="mb-3">
              <label for="title" class="form-label"
                >Judul Catatan <span class="text-danger"> *</span></label
              >
              <input
                v-model="title"
                type="text"
                class="form-control text-start text-white fst-normal fs-5"
                id="title"
                placeholder="Tuliskan judul catatan"
                autocomplete
              />
            </div>
            <div class="mb-3">
              <label for="content" class="form-label">Catatan</label>
              <textarea
                v-model="body"
                class="form-control text-start text-white fst-normal fs-6"
                id="content"
                rows="6"
                placeholder="Tuliskan isi catatan"
              ></textarea>
            </div>

            <div class="vstack gap-2 py-3">
              <button
                :disabled="!onDisabledButton"
                type="submit"
                title="Buat Catatan"
                class="btn btn-primary btn-md rounded"
              >
                Buat Catatan
              </button>
              <button
                type="reset"
                title="Batalkan"
                class="btn btn-danger btn-md rounded"
              >
                Batalkan
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["onSubmitNotes"],
  data() {
    return {
      title: "",
      body: "",
    };
  },
  computed: {
    onDisabledButton() {
      return Boolean(this.title) && Boolean(this.body);
    },
  },

  methods: {
    onSubmitHandler() {
      this.onSubmitNotes(this.title, this.body);

      this.title = "";
      this.body = "";
    },
  },
};
</script>

<style scoped>
input {
  width: 100%;
  height: 50px;
}
.form-control:hover {
  border: 1px groove #4c0bce;
}
.form-control:focus {
  border: 1px groove #4c0bce !important;
}
</style>
