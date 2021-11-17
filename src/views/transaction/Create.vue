<template>
  <div class="container my-5">
    <div class="row justify-content-center">
      <div class="col-8">
        <router-link to="/" class="btn btn-primary btn-sm rounded shadow mb-3"
          >Back</router-link
        >
        <div class="card rounded shadow">
          <div class="card-header">Create Transaction</div>
          <div class="card-body">
            <form @submit.prevent="store()">
              <div class="mb-3">
                <label for="" class="form-label">Title</label>
                <input type="text" class="form-control" v-model="transaction.title" />
                <div class="text-danger">Validation Message</div>
              </div>
              <div class="mb-3">
                <label for="" class="form-label">Amount</label>
                <input type="number" class="form-control" v-model="transaction.amount" />
                <div class="text-danger">Validation Message</div>
              </div>
              <div class="mb-3">
                <label for="" class="form-label">Time</label>
                <input
                  type="text"
                  class="form-control"
                  placeholder="yyyy-mm-dd hh:mm:ss"
                  v-model="transaction.time"
                />
                <div class="text-danger">Validation Message</div>
              </div>
              <div class="mb-3">
                <label for="" class="form-label">type</label>
                <select id="" class="form-select" v-model="transaction.type">
                  <option value="expense">Expense</option>
                  <option value="revenue">Revenue</option>
                </select>
                <div class="text-danger">Validation Message</div>
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
import axios from "axios";
import { reactive, ref } from "vue";
import { useRouter } from "vue-router";
export default {
  setup() {
    // data binding
    const transaction = reactive({
      title: '',
      amount: '',
      time: '',
      type: '',
    });

    const validation = ref([]);

    const router = useRouter();

    function store() {
      axios
        .post('http://course-laravel-akuntapi.test/api/transaction', transaction)
        .then(() => {
          router.push({
            name: "transaction.index",
          });
        })
        .catch((err) => {
          validation.value = err.response.data;
        });
    }

    return {
      transaction,
      validation,
      router,
      store,
    };
  },
};
</script>

<style>
</style>