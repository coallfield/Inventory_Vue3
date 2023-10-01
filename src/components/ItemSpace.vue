<template>
    <div class="items-place">
      <Desrciption @newCount="newCount" v-if="isDescription" v-model:show="isDescription"  :item="currentItem"></Desrciption>
            <div @drop="onDragDrop($event, n)" @dragover.prevent @dragenter.prevent v-for="n in 30" :key="n" class="items">
                <div @click="getItem(item)" v-for="item in items.filter(item => item.id === n && item.counter > 0)" class="wrapper-image">
                    <div v-if="item.id === n"  class="item-counter"> {{ item.counter }} </div>
                    <img v-if="item.id === n" @dragstart="onDragStart($event, item)" draggable="true" :src="item.image"> 
                </div>
            </div>
        </div>

</template>


<script>
import Desrciption from './Desrciption.vue';

 export default {
    props: {
        items: {
            type: Array,
            required: true
        }
    },
    data() {
      return {
          isDescription: false,
          currentItem: {}
      }
    },
    methods: {
        onDragStart(e, item) {
            e.dataTransfer.dropEffect = 'move';
            e.dataTransfer.effectAllowed = 'move';
            e.dataTransfer?.setData('itemId', item.id.toString());
        },
        onDragDrop(e, id) {
            const itemId = e.dataTransfer?.getData('itemId');
            this.items.map(item => {
                if (item.id === +itemId) {
                    item.id = id;
                }
                else if (item.id === id) {
                    item.id = +itemId;
                }
                localStorage.setItem('items', JSON.stringify(this.items));
            });
        },
        getItem(item) {
          this.isDescription = true
          this.currentItem = {...item}
        },
        newCount([count, item]) {
          this.$emit('newCount', [count, item])
        }
    },
    
    components: { Desrciption }
}
</script>

<style scoped>
.items-place {
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
        width: 45%;
        height: 75%;
        border: 1px solid white;
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        padding-right: 500px;
        .items{
        
            margin-left: 20px;
            margin-top: 20px;
            width: 120px;
            height: 120px;
            border: 1px solid grey;
            display: flex;
            justify-content: center;
            align-items: center;
            
        }

        .item-counter {
            color: white;
            position: absolute;
            text-align: center;
            margin: 10px, 10px;
            width: 25px;
            height: 25px;
            background-color: black;
            opacity: 50%;
            
        }
    }
</style>