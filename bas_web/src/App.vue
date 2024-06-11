<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
// import HeaderV1 from './components/HeaderV1.vue'
import { reactive } from 'vue';
import { useAuthStore } from './stores/auth';
// import { useTransferStore } from './stores/transfer';

const auth = useAuthStore()
// const transfer = useTransferStore()

const data = reactive({ //reactive untuk langsung merubah tampilan web, tanpa refresh.. misal counter langsung berubah
  // variable1: "test variable",
  // counter: 1,
  // variable2: [1, 2, 3, 4]
})

// const tambahCounter = () => {
//   data.counter++
// }
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logobankhope.png" width="125" height="100" />

    <div class="wrapper">
      <!-- <HeaderV1 :text="'Hello Vue, Bung Ahay'">
        <button @click="tambahCounter">Tambah Counter</button>
        Ini "Slot" Punya Bung Ahay {{ data.counter }}
        <p>
          Test Paragraf di Dalam Slot
        </p>
        <template #part1_header="{param1}">
          <h2>{{ param1 }}</h2>
        </template>
      </HeaderV1> -->
      {{ data.variable1 }}
      {{ data.variable2 }}
      <HelloWorld msg="Welcome to Bank Hope!" />

      <nav>
        <RouterLink v-if="auth.isLoggedIn" to="/">Home</RouterLink>
        <RouterLink v-if="auth.isLoggedIn" to="/about">About</RouterLink>
        <RouterLink v-if="!auth.isLoggedIn" to="/login">Login</RouterLink>
        <RouterLink v-if="auth.isLoggedIn" to="/transfer">Transfer</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
slop{
  color: red;
}

header {
  line-height: 1.5;
  max-height: 100vh;
  background-color: rgb(255, 240, 249);
  color: black;
  /* background-image: url("https://img.freepik.com/premium-vector/banking-finance-concept-illustration_387612-169.jpg") */
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  /* border: 10px solid rgb(188, 50, 215) */
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
