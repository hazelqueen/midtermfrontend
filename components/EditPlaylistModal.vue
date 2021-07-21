<template>
    <div>
        <b-modal id="editPlaylistModal" title="Music Entry" ok-title="Save Music" @ok="onSubmit">
            <form action="#">
                
                <b-form-group
                label="Enter title"
                label-for="title"
                >
                <b-form-input id="title" v-model="music.title" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Artist"
                label-for="artist"
                >
                <b-form-input id="artist" v-model="music.artist" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Genre"
                label-for="genre"
                >
                <b-form-input id="genre" v-model="music.genre" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Album"
                label-for="album"
                >
                <b-form-input id="album" v-model="music.album" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Date Released"
                label-for="date_released"
                >
                <b-form-input id="date_released" type="date" v-model="music.date_released" trim></b-form-input>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>
<script>
export default {
    props: {
        music: {}
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/musics/'+this.music.id, this.music)
                .then((res)=>{
                    if(res.status==202) {
                        alert('Updated successfully!!')
                    }
                })
                .catch((err)=> {
                    alert(err.message)
                })
        }
    }
}
</script>