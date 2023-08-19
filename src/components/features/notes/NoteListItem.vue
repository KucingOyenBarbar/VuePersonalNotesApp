<template>
  <div class="row justify-content-start g-2">
    <div class="col py-3">
      <MessageWarning :message="message" v-if="!items.length" />
      <div v-else class="row justify-content-arround g-3">
        <div
          class="col-12 col-lg-6 col-sm-10"
          v-for="(item, index) in items"
          :key="index"
        >
          <!-- <NoteItem :item="{ ...item }" :deleteNotes="deleteNotes" /> -->
          <div class="card nl_card_item">
            <div class="card-body">
              <div class="d-flex justify-content-end g-2">
                <span
                  v-if="!item.archived"
                  class="badge rounded-pill text-bg-success"
                  >Aktif</span
                >
                <span
                  v-if="item.archived"
                  class="badge rounded-pill text-bg-warning"
                  >Diarsipkan</span
                >
              </div>
              <div class="card-title text-start text-white fst-bolder fs-4">
                {{
                  item?.title.length > 50
                    ? `${item?.title.substring(0, 50)}...`
                    : item?.title
                }}
              </div>
              <div class="card-subtitle text-start text-white-50 fst-normal">
                {{ showFormatedData(item.createdAt) }}
              </div>
              <div class="card-text py-3">
                <p class="text-start text-white-50 fst-normal">
                  {{
                    item?.body.length > 120
                      ? `${item?.body.substring(0, 120)}...`
                      : item?.body
                  }}
                </p>
              </div>

              <div
                className="px-0 mx-0 position-absolute nl_card_item_button  px-3"
              >
                <div class="hstack gap-2">
                  <button
                    @click="deleteNotesHandler(index)"
                    type="button"
                    title="Hapus Catatan"
                    class="btn btn-danger btn-md"
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      height="1em"
                      viewBox="0 0 448 512"
                    >
                      <path
                        d="M135.2 17.7L128 32H32C14.3 32 0 46.3 0 64S14.3 96 32 96H416c17.7 0 32-14.3 32-32s-14.3-32-32-32H320l-7.2-14.3C307.4 6.8 296.3 0 284.2 0H163.8c-12.1 0-23.2 6.8-28.6 17.7zM416 128H32L53.2 467c1.6 25.3 22.6 45 47.9 45H346.9c25.3 0 46.3-19.7 47.9-45L416 128z"
                      />
                    </svg>
                  </button>
                  <button
                    v-if="!item.archived"
                    @click="archivedNotesHandler(item.id)"
                    type="button"
                    title="Arsipkan Catatan"
                    class="btn btn-warning btn-md"
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      height="1em"
                      viewBox="0 0 384 512"
                    >
                      <path
                        d="M0 48V487.7C0 501.1 10.9 512 24.3 512c5 0 9.9-1.5 14-4.4L192 400 345.7 507.6c4.1 2.9 9 4.4 14 4.4c13.4 0 24.3-10.9 24.3-24.3V48c0-26.5-21.5-48-48-48H48C21.5 0 0 21.5 0 48z"
                      />
                    </svg>
                  </button>

                  <button
                    v-if="item.archived"
                    @click="unArchivedNotesHandler(item.id)"
                    type="button"
                    title="Aktifkan Catatan"
                    class="btn btn-warning btn-md"
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      height="1em"
                      viewBox="0 0 512 512"
                    >
                      <path
                        d="M125.7 160H176c17.7 0 32 14.3 32 32s-14.3 32-32 32H48c-17.7 0-32-14.3-32-32V64c0-17.7 14.3-32 32-32s32 14.3 32 32v51.2L97.6 97.6c87.5-87.5 229.3-87.5 316.8 0s87.5 229.3 0 316.8s-229.3 87.5-316.8 0c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0c62.5 62.5 163.8 62.5 226.3 0s62.5-163.8 0-226.3s-163.8-62.5-226.3 0L125.7 160z"
                      />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import NoteItem from "./NoteItem.vue";
import MessageWarning from "@/components/shared/MessageWarning.vue";

export default {
  props: ["items"],
  components: {
    // NoteItem,
    MessageWarning,
  },
  data() {
    return {
      titleName: "Semua Daftar Catatan",
      message: "Belum Ada Daftar Catatan.",
      notes: this.items,
    };
  },
  methods: {
    showFormatedData(timestamps) {
      return new Date(timestamps).toLocaleDateString("id-ID", {
        timeZone: "Asia/Jakarta",
        dateStyle: "full",
      });
    },
    deleteNotesHandler(index) {
      this.notes.splice(index, 1);
    },
    archivedNotesHandler(noteId) {
      const items = this.items.find((note) => note.id === noteId);
      items.archived = true;
    },
    unArchivedNotesHandler(noteId) {
      const items = this.items.find((note) => note.id === noteId);
      items.archived = false;
    },
  },
};
</script>

<style scoped>
.nl_card_item {
  width: 100%;
  height: 200px !important;
  min-height: 250px;
  transition: ease 500ms;
  box-shadow: rgba(17, 17, 26, 0.05) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 0px 8px;
  overflow: hidden;
  position: relative;
}
.nl_card_item:hover {
  border: 1px groove #4c0bce;
}

.nl_card_item_button {
  position: absolute;
  bottom: 0;
  right: 0;
  padding: 20px;
}
</style>
