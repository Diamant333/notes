<template>
                 <div class="notes">
                   <div class="note" :class="[{ full: !grid }, note.impotCheck]" v-for="(note, index) in notes" :key="index">
                     <div class="note-header" :class="{ full: !grid }">

                        <input type="text" 
                        v-model="note.title" 
                        v-if="note.editable"
                        @keyup.enter= "note.editable=false; $emit('update')"
                        @keyup.esc= "note.editable=false; $emit('update'); note.title=titletemp;"
                        v-focus
                        >

                        <div v-else>
                            <p @click="note.editable=true; titletemp=note.title;">{{ note.title }}</p>
                        </div>
                       
                       <p style="cursor: pointer;" @click="removeNote(index)">X</p>
                     </div>
                     <div class="note-body">
                       <p>{{ note.descr }}</p>
                       <span>{{ note.date }}</span>
                     </div>
                   </div>
                 </div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
       
    },
    data() {
        return {
            titletemp: '',
            desctemp: ''
        }
    },
    methods: {
        removeNote (index) {
            console.log(`Note id - ${index} removed`)
            this.$emit('remove', index)
        },
        editTitle (index) {
           
            //console.log (`${note.editable}`)
            //this.$emit.editable = true
        }
    },
      directives: {
    focus: {
      inserted (el) {
        el.focus()
      }
    }
  }
}
</script>

<style lang="scss">

.hide {
    display: none;
}

.notes {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 40px 0;
    }
.note {
    width: 48%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: #ffffff;
    transition: all .25s cubic-bezier(.02,.01,.47,1);
    box-shadow: 0 30px 30px rgba(0,0,0,.02);
    &:hover {
        box-shadow: 0 30px 30px rgba(0,0,0,.04);
        transform: translate(0,-6px);
        transition-delay: 0s !important;

    }
    &.full {
        width: 100%;
        text-align: center;
    }
}
.note-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    h1 {
        font-size: 32px;
    }
    p {
        color: blue;
        font-size: 22px;
    }
    svg {
        margin-right: 12px;
        color: #999999;
        &.active {
            color: blue;
        }
        &:last-child  {
            margin-right: 0;
        }
    }
    &.full {
        justify-content: center;
        p {
            margin-right: 16px;
            &:last-child {
                margin-right: 0;
            }
        }
    }
}
.note-body {
    p {
    margin: 20px 0;
    }
    span {
        font-size: 14px;
        color: #999999;
    }
    

}
.important {
    background-color: #edf8539a;
}
.v-important {
    background-color: #fc616163;
}
</style>