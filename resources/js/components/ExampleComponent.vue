<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Example Component</div>

                    <div class="card-body">
                    <input type="text" v-model='item.name'><a href="#" v-on:click="add()">Add</a>
                    <ul v-for="item in items">
                        <li>{{item.id}}</li>
                        <li>{{item.name}}<a href="#" v-on:click="update(item.id)">Update</a><a href="#" v-on:click="remove(item.id)">Delete</a></li>
                    
                    </ul>
                        I'm an example2 component.
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
                return {
                    item : {
                        name : ''
                    },
                    items :[],
                }
        },
        methods:{
            getList(){
                axios.get('api/items').then(response => {
                    console.log(response);
                    this.items = response.data
                }).catch(err => console.log(err));

            },
            add()
            {
                axios.post('api/item/store',{ item : this.item }).then(response => {
                    console.log(response);
                    this.getList();
                }).catch(err => console.log(err));

            },
            update(id){
                axios.put('api/item/' + id,{
                    item : id
                }).then(response => {
                    console.log(response);
                }).catch(err => console.log(err));

            },
            remove(id){
                axios.delete('api/item/' + id,{
                    item : id
                }).then(response => {
                    console.log(response);
                }).catch(err => console.log(err));

            }

        },
        created(){
            this.getList();
        },
        mounted() {
            this.getList();
            console.log('Component 2mounted.')
        }
    }
</script>
