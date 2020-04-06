<template>
    <div class="new-note">
        <label>Title</label>
        <input type="text" v-model="note.title">
        <div class="radio">
            <table>
                <tr>
                    <td><input type="radio" name="importance" value="normal" checked v-model="note.impotCheck"></td>
                    <td>Нормальная</td>
                    <td><input type="radio" name="importance" value="important" v-model="note.impotCheck"></td>
                    <td style="color: darkgoldenrod;">Важная</td>
                    <td><input type="radio" name="importance" value="v-important" v-model="note.impotCheck"></td>
                    <td style="color: red;">Очень важная</td>
                </tr>
            </table>

        </div>
        <label>Description</label>
        <textarea name="" id="" cols="30" rows="10" v-model="note.descr"></textarea>
        
        <button class="btn btnPrimary" @click="addNote">New Note</button>

    </div>
</template>
<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        }
    },
    methods: {
        addNote () {
            this.$emit('addNote', this.note)
        }
    }
}
</script>

<style lang="scss">
.new-note {
    text-align: center;
    }
.new-note button {
    margin-top: 20px;
    margin-bottom: 20px;
}

</style>