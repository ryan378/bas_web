<script setup>
import { inject, reactive } from 'vue';
import router from '@/router/index';
import { VNumberInput } from 'vuetify/labs/VNumberInput'
// import { useTransferStore } from '@/stores/transfer';

// const transaction = useTransferStore()

const data = reactive({
    account_id: '',
    bank_id: '',
    amount: 0,
    transaction_date: '',
    snackbar: false,
    pesanTransfer: ''
})

const myAxios = inject('myAxios')

const transfer = () => {
    console.log('transfer clicked', data);
    
    myAxios.post('/transaction/transfer-bank', {
        account_id: data.account_id,
        bank_id: data.bank_id,
        amount: data.amount,
        transaction_date: data.transaction_date
    }).then((res) => {
        if (res.status == 200){
            data.pesanTransfer = "Anda Berhasil Transfer"
            router.push('transfer')
        }
        data.snackbar = true
    }, () => {
        data.pesanTransfer = "Transfer Anda Gagal"
        data.snackbar = true
    })
}
</script>

<template>
  <div class="container">
      <div>
          <label>Account ID</label>
          <v-text-field type="text" v-model="data.account_id"></v-text-field>
      </div>
      <div>
          <label>Bank ID</label>
          <v-text-field type="text" v-model="data.bank_id"></v-text-field>
      </div>
      <div>
          <label>Amount</label>
          <v-number-input v-model="data.amount"></v-number-input>
      </div>
      <div>
          <label>Transaction Date</label>
          <v-text-field type="text" v-model="data.transaction_date"></v-text-field>
      </div>
      <v-card class="pa-5">
          <div>
              <v-btn @click="transfer">
                  Kirim Transfer
              </v-btn>
          </div>
      </v-card>
      <v-snackbar v-model="data.snackbar">
          {{ data.pesanTransfer }}

          <template v-slot:actions>
              <v-btn color="pink" variant="text" @click="snackbar = false">
              Close
              </v-btn>
          </template>
      </v-snackbar>
  </div>
</template>

<!-- <template>
    <form @submit.prevent="submitForm" class="transaction-form">
      <div class="form-group">
        <label for="AccountID">Account ID:</label>
        <input type="text" id="AccountID" v-model="formData.AccountIDID" required>
      </div>
      
      <div class="form-group">
        <label for="BankID">Bank ID:</label>
        <input type="text" id="BankID" v-model="formData.BankID" required>
      </div>
  
      <div class="form-group">
        <label for="Amount">Amount Transfer:</label>
        <input type="numeric" id="Amount" v-model="formData.Amount" required>
      </div>
  
      <div class="form-group">
        <label for="date">Transaction Date:</label>
        <input type="date" id="date" v-model="formData.Date" required>
      </div>
      
      <button type="submit">Send</button>
    </form>
</template>
  
<script>
  export default {
    data() {
      return {
        formData: {
          AccountID: '',
          BankID: '',
          Amount: '',
          Date: ''
        }
      };
    },
    methods: {
      submitForm() {
        // Proses data formulir di sini
        console.log('Data formulir transfer:', this.formData);
      }
    }
  };
  </script>
  
  <style scoped>
  .transaction-form {
    width: 300px;
    margin: auto;
  }
  
  .form-group {
    margin-bottom: 20px;
    border-bottom: 1px solid #ccc; /* Tambahkan border antara setiap form-group */
    padding-bottom: 10px; /* Tambahkan padding bawah untuk ruang antara form-group */
  }
  
  .form-group label {
    display: block;
    margin-bottom: 5px;
  }
  
  .form-group input {
    width: 100%;
    padding: 8px;
    border: none; /* Hilangkan border pada input */
    border-radius: 4px;
    box-sizing: border-box;
    outline: none; /* Hilangkan  outline  */
  }
  
  button[type="submit"] {
    background-color: #4CAF50;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button[type="submit"]:hover {
    background-color: #45a049;
  }
</style> -->