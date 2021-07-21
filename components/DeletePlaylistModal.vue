<template>
    <div>
        <b-modal id="deletePlaylistModal" title="Music Entry" ok-title="Delete Music" @ok="onDelete" ok-variant="danger">
            You sure you want to delete this music? <br>
            {{music.title}} <br> {{music.artist}}
        </b-modal>
    </div>
</template>
<script>
export default {
    props: {
        music: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/musics/'+this.music.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Music deleted!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>
