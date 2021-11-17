<template>
  <div class="container my-5">
    <div class="row justify-content-center">
      <div class="col-8">
        <router-link to="/create" class="btn btn-primary btn-sm rounded shadow mb-3"
          >Add</router-link
        >
        <div class="card rounded shadow">
          <div class="card-header">Transaction List</div>
          <div class="card-body">
            <table class="table">
              <thead>
                <tr>
                  <td>Title</td>
                  <td>Amount</td>
                  <td>Type</td>
                  <td>Action</td>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(transaction, index) in transactions.data"
                  :key="index"
                >
                  <td>{{ transaction.title }}</td>
                  <td>{{ transaction.amount }}</td>
                  <td>{{ transaction.type }}</td>
                  <td>
                    <div class="btn-group">
                      <router-link
                        :to="'/edit/' + transaction.id"
                        class="btn btn-small btn-outline-info"
                        >Edit</router-link
                      >
                      <button class="btn btn-small btn-outline-danger">
                        Delete
                      </button>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
// onmounted semacam hook untuk menarik data lalu ingin melakukan apa
import { onMounted, ref } from "vue";

export default {
  setup() {
    // reactive state
    let transactions = ref([]);

    onMounted(() => {
      // get data from api endpoint
      axios
        .get("http://course-laravel-akuntapi.test/api/transaction")
        .then((result) => {
          transactions.value = result.data;
        })
        .catch((err) => {
          console.log(err.response);
        });
    });

    return {
      transactions,
    };
  },
};
</script>

<style>
</style>