<template>
   <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <!-- <a href="/create">tes</a> -->
                <router-link 
                    :to="{ name: 'transaction.index'}" class="btn btn-primary btn-sm rounded shadow mb-3"
                >Back</router-link>
                <div class="card rounded shadow">
                    <div class="card-header">
                        Create Transaction
                    </div>
                    <div class="card-body">
                        <form @submit.prevent="store()">
                            <div class="mb-3">
                                <label for="" class="form-label">Title</label>
                                <!-- directive v model -->
                                <input type="text" class="form-control" v-model="transaction.title">
                                <!-- directive if  validation memangggil dari catch(err)-->
                                <div v-if="validation.title" class="text-danger">
                                    {{ validation.title[0] }}
                                </div>
                            </div>
                            <div class="mb-3">
                                <label for="" class="form-label">Amount</label>
                                <input type="number" class="form-control" v-model="transaction.amount">
                                <div v-if="validation.amount" class="text-danger">
                                    {{ validation.amount[0] }}
                                </div>
                            </div>
                            <div class="mb-3">
                                <label for="" class="form-label">Time</label>
                                <input type="text" class="form-control" placeholder="yyyy-mm-dd hh:mm:ss" v-model="transaction.time">
                                <div v-if="validation.time" class="text-danger">
                                    {{ validation.time[0] }}
                                </div>
                            </div>
                            <div class="mb-3">
                                <label for="" class="form-label">Type</label>
                                <select id="" class="form-select" v-model="transaction.type">
                                    <option value="expense">Expense</option>
                                    <option value="revenue">Revenue</option>
                                </select>
                                <div v-if="validation.type" class="text-danger">
                                    {{ validation.type[0] }}
                                </div>
                            </div>
                            <button class="btn btn-outline-primary">Submit</button>
                        </form>          
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
//reactive untuk data binding
import { reactive, ref } from 'vue'
import { useRouter } from 'vue-router'
//axios request ke api endpoint
import axios from 'axios'
export default {
    setup() {
        //data lbinding
        const transaction = reactive({
            title: '',
            amount: '',
            time: '',
            type: ''
        });
        const validation = ref([]);
        //redirect ke halaman index jika berhasil
        const router = useRouter();
        //request ke api dengan data create
        function store(){
            axios.post(
                'http://127.0.0.1:8000/api/transaction',
                //dari setup
                transaction
            )
            .then(() =>{
                router.push({
                    name: 'transaction.index'
                });
            }).catch((err)=>{
                validation.value = err.response.data
            });
        }
        return {
            transaction,
            validation,
            router,
            store
        }
    }
}
</script>