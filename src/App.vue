<!-- eslint-disable vue/no-deprecated-html-element-is -->
<template>
  <HeaderNav />
  <main>
    <div class="container position-relative">
      <div class="row justify-content-center g-2 py-5">
        <div class="col-12 col-lg-8 col-md-10">
          <NoteFormInput :onSubmitNotes="onSubmitNoteHandler" />

          <div class="row justify-content-start g-2 py-3">
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
                @click="onArchivedNotes"
                type="button"
                class="btn btn-outline-primary btn-md rounded-pill text-white"
              >
                Diarsipkan
              </button>
            </div>
          </div>

          <div v-if="isNotes">
            <HeadingTitle title="Semua Daftar Catatan" />
            <div class="row justify-content-start g-2 py-3">
              <div class="col">
                <div class="input-group mb-3">
                  <input
                    type="text"
                    class="form-control"
                    placeholder="Cari Catatan..."
                    aria-label="Cari Catatan..."
                    v-model="searchValues"
                  />
                </div>
              </div>
            </div>

            <NoteListItemVue
              :items="
                initialData
                  .filter(
                    (item) =>
                      item.title
                        .toLowerCase()
                        .includes(searchValues.toLowerCase()) ||
                      item.body
                        .toLowerCase()
                        .includes(searchValues.toLowerCase())
                  )
                  .sort((a, b) => b.createdAt.localeCompare(a.createdAt))
              "
            />
          </div>
          <div v-if="isActiveNotes">
            <HeadingTitle title="Catatan Aktif" />
            <div class="row justify-content-start g-2 py-3">
              <div class="col">
                <div class="input-group mb-3">
                  <input
                    type="text"
                    class="form-control"
                    placeholder="Cari Catatan..."
                    aria-label="Cari Catatan..."
                    v-model="searchValues"
                  />
                </div>
              </div>
            </div>

            <NoteListItemVue
              :items="
                initialData
                  .filter((item) => !item.archived)
                  .filter(
                    (item) =>
                      item.title
                        .toLowerCase()
                        .includes(searchValues.toLowerCase()) ||
                      item.body
                        .toLowerCase()
                        .includes(searchValues.toLowerCase())
                  )
                  .slice()
                  .sort((a, b) => b.createdAt.localeCompare(a.createdAt))
              "
            />
          </div>
          <div v-if="isArchivedNotes">
            <HeadingTitle title="Catatan Diarsipkan" />
            <div class="row justify-content-start g-2 py-3">
              <div class="col">
                <div class="input-group mb-3">
                  <input
                    type="text"
                    class="form-control"
                    placeholder="Cari Catatan..."
                    aria-label="Cari Catatan..."
                    v-model="searchValues"
                  />
                </div>
              </div>
            </div>

            <NoteListItemVue
              :items="
                initialData
                  .filter((item) => item.archived)
                  .filter(
                    (item) =>
                      item.title
                        .toLowerCase()
                        .includes(searchValues.toLowerCase()) ||
                      item.body
                        .toLowerCase()
                        .includes(searchValues.toLowerCase())
                  )
                  .sort((a, b) => b.createdAt.localeCompare(a.createdAt))
              "
            />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import HeaderNav from "./components/shared/HeaderNav.vue";
import NoteListItemVue from "./components/features/notes/NoteListItem.vue";
import NoteFormInput from "./components/features/notes/NoteFormInput.vue";
import HeadingTitle from "@/components/shared/HeadingTitle.vue";
import { nanoid } from "nanoid";

export default {
  name: "App",
  components: {
    HeaderNav,
    NoteListItemVue,
    NoteFormInput,
    HeadingTitle,
  },

  data() {
    return {
      initialData: [
        {
          id: 1,
          title: "Babel",
          body: "Babel merupakan tools open-source yang digunakan untuk mengubah sintaks ECMAScript 2015+ menjadi sintaks yang didukung oleh JavaScript engine versi lama. Babel sering dipakai ketika kita menggunakan sintaks terbaru termasuk sintaks JSX.",
          createdAt: "2022-04-14T04:27:34.572Z",
          archived: false,
        },
        {
          id: 2,
          title: "Functional Component",
          body: "Functional component merupakan React component yang dibuat menggunakan fungsi JavaScript. Agar fungsi JavaScript dapat disebut component ia harus mengembalikan React element dan dipanggil layaknya React component.",
          createdAt: "2022-04-14T04:27:34.572Z",
          archived: true,
        },
        {
          id: 3,
          title: "Modularization",
          body: "Dalam konteks pemrograman JavaScript, modularization merupakan teknik dalam memecah atau menggunakan kode dalam berkas JavaScript secara terpisah berdasarkan tanggung jawabnya masing-masing.",
          createdAt: "2022-04-14T04:27:34.572Z",
          archived: true,
        },
        {
          id: 4,
          title: "Lifecycle",
          body: "Dalam konteks React component, lifecycle merupakan kumpulan method yang menjadi siklus hidup mulai dari component dibuat (constructor), dicetak (render), pasca-cetak (componentDidMount), dan sebagainya. ",
          createdAt: "2022-04-14T04:27:34.572Z",
          archived: false,
        },
        {
          id: 5,
          title: "ESM",
          body: "ESM (ECMAScript Module) merupakan format modularisasi standar JavaScript.",
          createdAt: "2022-04-14T04:27:34.572Z",
          archived: false,
        },
        {
          id: 6,
          title: "Module Bundler",
          body: "Dalam konteks pemrograman JavaScript, module bundler merupakan tools yang digunakan untuk menggabungkan seluruh modul JavaScript yang digunakan oleh aplikasi menjadi satu berkas.",
          createdAt: "2022-04-14T04:27:34.572Z",
          archived: true,
        },
      ],
      isNotes: true,
      isArchivedNotes: false,
      isActiveNotes: false,
      searchValues: "",
    };
  },

  methods: {
    onNotes() {
      this.isNotes = true;
      this.isArchivedNotes = false;
      this.isActiveNotes = false;
    },
    onArchivedNotes() {
      this.isArchivedNotes = true;
      this.isActiveNotes = false;
      this.isNotes = false;
    },
    onActiveNotes() {
      this.isActiveNotes = true;
      this.isArchivedNotes = false;
      this.isNotes = false;
    },

    onSubmitNoteHandler(title, body) {
      if (Boolean(title) && Boolean(body)) {
        const newNotes = {
          id: nanoid(16),
          title,
          body,
          archived: !true,
          createdAt: new Date().toISOString(),
        };

        this.initialData.push(newNotes);
      }
    },

    deleteNotesHandler(index) {
      this.initialData.splice(index, 1);
    },
  },
};
</script>

<style scoped>
input {
  height: 50px;
}
</style>
