<template>
  <div class="row justify-content-center g-2 py-3">
    <div class="hstack gap-2">
      <button
        @click="onNotes"
        type="button"
        class="btn btn-outline-primary btn-md rounded-pill text-white"
      >
        Semua
      </button>
      <button
        @click="onActiveNotes"
        type="button"
        class="btn btn-outline-primary btn-md rounded-pill text-white"
      >
        Catatan Aktif
      </button>
      <button
        @click="setMyNotes"
        type="button"
        class="btn btn-outline-primary btn-md rounded-pill text-white"
      >
        Diarsipkan {{ isArchivedNotes }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NoteTabButton",
  props: ["isNotes", "archivedNotes"],
  data() {
    return {
      myNotes: this.isNotes,
      isArchivedNotes: this.archivedNotes,
    };
  },

  methods: {
    setMyNotes() {
      this.isArchivedNotes = true;
    },
  },
};
</script>

<style></style>
