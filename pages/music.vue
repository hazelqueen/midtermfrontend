<template>
    <div>
        <NavBar />
        <EditPlaylistModal :music="selectedMusic" />
        <DeletePlaylistModal :music="selectedMusic" @onDeleted="getAll"/>
        <div class="container">
            <h1>
                Music
                <PlaylistEntryModal class="float-right" @onAdd="getAll"/>
            </h1>

            <table class="table table-bordered table-stripped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>ID</th>
                        <th>Title</th>
                        <th>Artist</th>
                        <th>Genre</th>
                        <th>Album</th>
                        <th>Date Released</th>
                        <th>&nbsp;</th>
                        
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="music in musics" :key="music.id">
                        <td>{{music.id}}</td>
                        <td>{{music.title}}</td>
                        <td>{{music.artist}}</td>
                        <td>{{music.genre}}</td>
                        <td>{{music.album}}</td>
                        <td>{{music.date_released}}</td>
                        <td>
                            <b-button @click="onEdit(music)" variant="info" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(music)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>

                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import EditPlaylistModal from '~/components/EditPlaylistModal.vue'
export default {
  components: { EditPlaylistModal },
    data() {
        return {
            musics: [],
            selectedMusic: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/musics')
            .then((res)=>{
                if(res.status==200) {
                    this.musics =res.data
                }
            })
        },
        onEdit(selectedMusic) {
            this.selectedMusic = selectedMusic;
            this.$bvModal.show('editPlaylistModal')
        },
        onDelete(selectedMusic) {
            this.selectedMusic = selectedMusic;
            this.$bvModal.show('deletePlaylistModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>