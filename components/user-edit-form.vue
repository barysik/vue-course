<template>
    <div class="template-wrapper">
        <form>
            <div class="form-group">
                <label for="firstName">First Name</label>
                <input type="text" class="form-control" id="firstName" placeholder="Enter First Name" v-model="user.firstName">
            </div>
            <div class="form-group">
                <label for="lastName">Last Name</label>
                <input type="text" class="form-control" id="lastName" placeholder="Enter Last Name" v-model="user.lastName">
            </div>
            <div class="form-group">
                <label for="email">Email address</label>
                <input type="email" class="form-control" id="email" placeholder="Enter email" v-model="user.email">
            </div>
            <button type="button" class="btn btn-primary"  v-on:click="saveUser">Save</button>
        </form>
    </div>
</template>

<script>
    module.exports = {
        props: {
            id: {
                type: Number,
                required: true
            }
        },
        data: function() {
            return { 
                user: {}
            }
        },
        mounted: function () {
            this.loadUser(this.id);
        },
        methods: {
             saveUser: function () {
                this.$emit('save-user');
             },
             loadUser: function (id) {
                var self = this;
                axios.get('http://localhost:3000/users?id=' + id)
                    .then(function (response) {
                        self.user = response.data[0];
                    });
             }
        }
    }
</script>

<style>

</style>