<template>
    <div class="template-wrapper"> 
        <table class="table table-striped">
        <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Avatar</th>
                <th scope="col">First Name</th>
                <th scope="col">Last Name</th>
                <th scope="col">E-mail</th>
                <th scope="col">Actions</th>
            </tr>
        </thead>
        <tbody > 
            <tr v-for="(user, index) in users" :key="user.id">
                <th scope="row">{{index + 1}}</th>
                <td>
                    <img v-bind:src="userAvatar(user)" height="50">
                </td>
                <td>{{user.firstName | toUpperCase}}</td>
                <td>{{user.lastName | toUpperCase}}</td>
                <td>{{user.email}}</td>
                <td>
                    <button type="button" class="btn btn-dark" v-copy="user.firstName + ' ' +user.lastName" v-tooltip.top="'Copy'">
                        <i class="fa fa-copy"></i>
                    </button>
                    <button type="button" class="btn btn-primary" v-tooltip.right="'Edit'" v-on:click="editUser(user.id)">
                        <i class="fa fa-edit"></i>
                    </button>
                </td>
            </tr>
        </tbody>
        </table>

        <p> 
            <span>Count of Users: {{countOfUsers}}</span>
        </p>
    </div>
    
</template>

<script>
    module.exports = {
        props: {
            users: {
                type: Array,
                required: true
            }
        },
        data: function() {
            return {
                defaultAvatarLink: 'resources/images/default-avatar.png'
            }
        },
        computed: {
            countOfUsers: function () {
                return this.users.length;
            }
        },
        methods: {
             userAvatar: function (user) {
                 return user.picture || this.defaultAvatarLink;
             },
             editUser: function (id) {
                this.$emit('edit-user', id);
             }
        },
        filters: {
            toUpperCase: function (value) {
                if (!value) return ''
                return value.toUpperCase()
            }
        }
    }
</script>

<style>

</style>