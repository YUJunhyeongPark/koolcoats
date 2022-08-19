<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Welcome to Koolcoats
        </p>
        <p class="subtitle">
          The best coat store online
        </p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest Products</h2>
      </div>


      <div class="column is-3" v-for="product in latestProducts" v-bind:key="product.id">
        <div class="box">
          <figure class="image mb-4">
            <img v-bind:src="product.get_thumbnail">
          </figure>

          <h3 class="is-size-4">{{ product.name }}</h3>
          <p class="is-size-6 has-text-grey">${{ product.price }}</p>

          <router-link v-bind:to="product.get_absolute_url" class="button is-dark mt-4">View Details</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HomeView',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
  },
  mounted() {
    this.getLatestProducts()
  },
  methods: {
    getLatestProducts() {
      axios({
        method: 'get',
        url: 'http://127.0.0.1:8000/api/v1/latest-products/',
        auth: {
          username: 'oakr0414',
          password: 'aortm9606'
        }
      }).then(response => {
        this.latestProducts = response.data
      }).catch(error => {
        console.log(error)
      })
    }
  }
}
</script>

<stype scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</stype>
