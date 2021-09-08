<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">ToDo List</h2>

            <!-- Formulario -->
            <add-item-form
                v-on:reloadlist="getList()"
            />
        </div>

        <!-- Lista View -->
        <list-view
            :items="items"
            v-on:reloadlist="getList()
        "/>
    </div>
</template>

<script>
import addItemForm from './addItemForm.vue';
import ListView from './listView.vue';

export default {
    components: {
        addItemForm,
        ListView,
    },
    data: function() {
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
            .then(response => {
                this.items = response.data
            })
            .catch(error => {
                console.log(error);
            })
        }
    },
    created() {
        this.getList();
    }
}
</script>

<style>
.todoListContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #dfdfdf;
    padding: 10px;
}

#title {
    text-align: center;
}
</style>