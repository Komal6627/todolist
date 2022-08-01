<template>
<main class="flex justify-center w-full h-screen">
    <div>
        <form @submit="formSubmit" class="bg-gray-100 border-blue-400 rounded-lg border-2 px-12">
            <table>
                <h2 class="text-teal-900 text-xl font-bold pt-6">Information Form</h2>
                <hr />
                <br />
                <label class="pt-10 py-10 " for="firstname">First name:</label><br />
                <input type="text" v-model="user.firstname" id="firstname" name="firstname" placeholder="Enter your first name" /><br /><br />
                <label for="lastname">Last name:</label><br />
                <input type="text" v-model="user.lastname" id="lastname" name="lastname" placeholder="Enter your Last name" /><br /><br />
                <label for="address"> address: </label><br />
                <input type="text" v-model="user.address" id="address" name="address" placeholder="Enter your address" />
                <br /><br />
                <label for="number">Phone Number: </label><br />
                <input type="number" v-model="user.number" id="number" name="number" placeholder="Enter your number" />
                <br /><br />
                <label for="text">City: </label><br />
                <input type="text" v-model="user.city" id="city" name="city" placeholder="Enter your city" />
                <br /><br />
                <div>
                    <button class="py-1 px-5 mr-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3" type="submit" @click="formSubmit"> Submit </button>
                    <button class="py-1 px-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3" type="reset"> Reset </button>
                </div>
            </table>
        </form>
        <br>
        <table class="list">
            <tr>
                <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
                <th class="px-4 border-blue-400 rounded-lg border-4">First Name</th>
                <th class="px-4 border-blue-400 rounded-lg border-4">Last Name</th>
                <th class="px-4 border-blue-400 rounded-lg border-4">Address</th>
                <th class="px-4 border-blue-400 rounded-lg border-4">City</th>
                <th class="px-4 border-blue-400 rounded-lg border-4">Contact No</th>
                <th class="px-4 border-blue-400 rounded-lg border-4">Action</th>
            </tr>
            <tr v-for="(item,index) in users" v-bind:index="index" :key="item">
                <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
                <td class="px-4 border-blue-400 rounded-lg border-4">{{item.firstname}}</td>
                <td class="px-4 border-blue-400 rounded-lg border-4">{{item.lastname}}</td>
                <td class="px-4 border-blue-400 rounded-lg border-4">{{item.address}}</td>
                <td class="px-4 border-blue-400 rounded-lg border-4">{{item.city}}</td>
                <td class="px-4 border-blue-400 rounded-lg border-4">{{item.number}}</td>
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
                firstname: '',
                lastname: '',
                address: '',
                city: '',
                number: '',
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
                firstname: '',
                lastname: '',
                address: '',
                city: '',
                number: ''
            };
        },
        onReset(event) {
            event.preventDefault();
            this.form.email = "";
            this.form.name = "";
            this.form.address = "";
            this.form.contact = "";
            this.form.city=""
        },
        userDelete(index) {
            this.users.splice(index, 1)
        },
        onEdit(index){
            this.user.firstname=this.users[index].firstname;
            this.user.lastname=this.users[index].lastname;
            this.user.address=this.users[index].address;
            this.user.city=this.users[index].city;
            this.user.number=this.users[index].number;
            this.isEdit=true;
            this.indexEdit=index;
        },
    }
}
</script>