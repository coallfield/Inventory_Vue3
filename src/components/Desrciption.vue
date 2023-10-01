<template>
    <div class="description">
        <div class="header">
            <button @click="this.$emit('update:show', false)" class="close">×</button>
            <div class="image-wrap-description">
                <img class="image-in-descr" :src="item.image" >
                <div class="title-item">{{item.name}}</div>
                <div class="item-description">{{ item.body }}</div>
            </div>
        </div>
        <div v-if="!wrong" class="counter"> You have {{ item.counter }}</div>
        <div v-if="wrong" class="counter"> Enter a number! </div>
        <MyButton v-if="!isDeleteItems" @click="isDeleteItems = true" class="btns"> Delete </MyButton>
        <div v-if="isDeleteItems" class="delete-counter">
            <input @input="deleteItems = $event.target.value" :value="afterClick" placeholder="How many items to remove?" type="text">
            <MyButton @click="getValue" class="btns" style="width: 50%;"> Confirm </MyButton>
        </div>

    </div>
</template>

<script>
export default {
    props: {
        item: {
            type: Object,
            required: true
        },
        show: {
            type: Boolean
        }
    },
    data() {
        return {
            isDeleteItems: false,
            wrong: false,
            deleteItems: ''
        }
    },
    methods: {
        getValue() {
            const afterClick = ''
            if(this.deleteItems.match(/[^0-9 ]/g, '') || this.deleteItems.trim() === '') {
                this.wrong = true
                setTimeout(() => {
                    this.wrong = false
                }, 1000)
                return
            }
            this.item.counter = this.item.counter - +this.deleteItems
            if(this.item.counter < 0) {
                this.item.counter = 0
            }
            this.$emit('newCount', [+this.deleteItems, this.item])
            this.$emit('update:show', false)
        }
    }

}
</script>

<style scoped lang="scss">
    .description {
        width: 50%;
        height: 100%;
        background-color: black;
        z-index: 998;
        position: absolute;
        .header {
            .close {
                
                color: white;
                font-size: 3rem;
                margin: 10px;
                background-color: none;
                outline: none;
                background: none;
                border: none
            }
            .image-wrap-description {
                display: flex;
                justify-content: center;
                align-items: center;
                flex-direction: column;
                grid-gap: 20px;
                width: 50%;
                height: 30vh;
                margin-top: 30px;
                margin-left: auto;
                margin-right: auto;
                .image-in-descr {
                    width: 120px;
                    height: 180px;
                }

                .title-item {
                    color: white;
                    font-size: 3rem;
                    width: 450px;
                    text-align: center;
                }
                .item-description {
                    width: 400px;
                    text-align: center;
                    word-break: break-all;
                    color: white;
                    font-size: 1.5rem;

                }
            }
        }
        .btns {
        font-size:1.5rem;
        position: absolute;
        bottom: 0;
        width: 95%;
        height: 5vh;   
    }
        .delete-counter {
            width: 100%;
            position: absolute;
            bottom: 0;
            padding: 10px;
            input {
                text-align: center;
                color: white;
                background: none;
                border: 2px solid white;
                outline: none;
                border-radius: 5px;
                width: 45%;
                height: 5vh;   
            }
        }
        .counter {
            position: absolute;
            bottom: 70px;
            width: 100%;
            text-align: center;
            color: red;
            font-size: 1.5rem;
            margin-top: 50px;

        }
    }
</style>