<template>
  <div class="app">

    <MyButton  @click="clearStorage()">
        Clear local Storage
    </MyButton>

    <ItemSpace @newCount="newCount" :items="items"></ItemSpace>
    </div>
</template>

<script>
import ItemSpace from './components/ItemSpace.vue';

export default {
    data() {
        return {
            items: JSON.parse(localStorage.getItem('items')) || [
                { name: 'Red Card', body: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum sit amet magna quam. Mauris semper ante massa. Pellentesque elementum ante ligula, nec aliquam elit aliquam ut.', image: './src/img/redItem.png', counter: 4, id: 1 },
                { name: 'Green Card', body: 'Etiam rutrum urna in felis condimentum, eget ultricies arcu pellentesque. Nulla sit amet pretium turpis.', image: './src/img/greenItem.png', counter: 2, id: 2 },
                { name: 'Blue Card', body: 'Cras vestibulum placerat ex, vitae rhoncus quam sollicitudin eget. Integer pellentesque ultrices finibus. Pellentesque euismod leo elit, vitae feugiat massa dignissim sit amet.', image: './src/img/blueItem.png', counter: 1, id: 3 }
            ]
            
        }
    },
    methods: {
        clearStorage() {
            localStorage.clear();
            this.items = [
                { name: 'Red Card', body: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum sit amet magna quam. Mauris semper ante massa. Pellentesque elementum ante ligula, nec aliquam elit aliquam ut.', image: './src/img/redItem.png', counter: 4, id: 1 },
                { name: 'Green Card', body: 'Etiam rutrum urna in felis condimentum, eget ultricies arcu pellentesque. Nulla sit amet pretium turpis.', image: './src/img/greenItem.png', counter: 2, id: 2 },
                { name: 'Blue Card', body: 'Cras vestibulum placerat ex, vitae rhoncus quam sollicitudin eget. Integer pellentesque ultrices finibus. Pellentesque euismod leo elit, vitae feugiat massa dignissim sit amet.', image: './src/img/blueItem.png', counter: 1, id: 3 }
            ]
        },
        newCount([count, item]) {
            this.items.forEach(i => {
                if(i.name === item.name) {
                    i.counter = i.counter - +count
                    if(i.counter < 0) {
                        i.counter = 0
                    }
                    localStorage.setItem('items', JSON.stringify(this.items))
                }
            })
        }
    },
    components: { ItemSpace }
}
</script>

<style lang="scss">
* {
  
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}


.app {
    width: 100%;
    height: 100vh;
    background-color: black;
    .btns {
        color: white;
        margin: 10px;
        background: none;
        border: 2px solid white;
        outline: none;
        border-radius: 5px;
        width: 10%;
        height: 5vh;   
    }
    .over-btns {
        color: black;
        margin: 10px;
        background: white;
        border: 2px solid white;
        outline: none;
        border-radius: 5px;
        width: 10%;
        height: 5vh;
    }
}



</style>