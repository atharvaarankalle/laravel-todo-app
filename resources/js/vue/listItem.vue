<template>
    <div>
        <div class="item">
            <input 
                type="checkbox"
                @change="updateCheck()"
                checked="{{ item.completed }}"
            />
            <span :class="[item.completed ? 'complete' : 'incomplete', 'itemText']">{{ item.name }}</span>
            <button @click="removeItem()" class="deleteButton">
                <font-awesome-icon icon="trash" />
            </button>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if (response.status == 200) {
                    this.$emit('itemChanged');
                }
            })
            .catch( error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
    .complete {
        text-decoration: line-through;
        color: #999999;
    }

    .itemText {
        width: 100%;
        margin-left: 20px;
    }

    .item {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .deleteButton {
        background: #e6e6e6;
        border: none;
        color: #FF0000;
        outline: none;
    }
</style>