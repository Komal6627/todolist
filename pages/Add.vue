<template>
<main class="flex justify-center w-full h-screen">
    <div>
        <form @submit="formSubmit" class="bg-gray-100 border-blue-400 rounded-lg border-2 px-12">
            <table>
                <h2 class="text-teal-900 text-xl font-bold pt-6">Information Form</h2>
                <hr />
                <br />
                <label class="pt-10 py-10 " for="taskname">Task name:</label><br />
                <input type="text" v-model="user.taskname" id="taskname" name="taskname" placeholder="Enter your task" /><br /><br />
                <br /><br />
                <div>
                    <button class="py-1 px-5 mr-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3" type="submit" @click="formSubmit"> Submit </button>
                    <button class="py-1 px-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3" type="reset"> Reset </button>
                </div>
            </table>
        </form>
        <br>
        <table class="list">
            <tr v-for="(item,index) in users" v-bind:index="index" :key="item">
                 <td class="px-4 border-blue-400 rounded-lg border-4">{{item.taskname}}</td>
                <td class="px-4 border-blue-400 rounded-lg border-4">{{item.Action}}
                    <button class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20" @click="userDelete(index)">
                        Delete
                    </button>
                    <button class="mx-3 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20" @click="onEdit(index)">
                        Edit
                    </button>
                    <!-- <button class="mx-3 rounded-lg bg-teal-300 hover:bg-teal-300 text-white w-20" @click="onsSearch(index)">
                        Search
                    </button> -->
                </td>
            </tr>
        </table>
    </div>
</main>
</template>
<script>
export default {
    data() {
        return {
            isEdit:false,
            indexEdit:-1,
            users: [],
            user: {
               taskname: ' '
            },
        };
    },
    methods: {
        formSubmit(event) {
            event.preventDefault();
            if(this.isEdit==true){
                this.users[this.indexEdit]=this.user;
                this.isEdit=false;
                this.indexEdit=-1;
            }
            else{
                 this.users.push(this.user);
            }
           this.user = {
                taskname: ' '
            };
        },
        onReset(event) {
            event.preventDefault();
            this.form.taskname = "";
        },
        userDelete(index) {
            this.users.splice(index, 1)
        },
        onEdit(index){
            this.user.taskname=this.users[index].taskname;
            this.isEdit=true;
            this.indexEdit=index;
        },
    }
}
</script>
