<template>
  <div>
    <div v-if="productList.length == 0">
      <h5 style="text-align: center">Kayıtlı ürün bulunamadı.</h5>
    </div>
    <div class="row product-container">
      <app-product v-for="product in productList">
        <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
        <div class="card-body">
          <h5 class="card-title">{{ product.title }}</h5>
          <small>
            <strong>Adet : </strong> {{ product.count }}
          </small>
          <br>
          <small>
            <strong>Fiyat : </strong> {{ product.price }}
          </small>
          <br>
          <small>
            <strong>Tutar : </strong> {{ product.totalPrice }}
          </small>
        </div>
      </app-product>
    </div>
  </div>
</template>
<script>
import Product from "./Product";
import {eventBus} from "../main";

export default {
  components: {
    appProduct: Product
  },
  data() {
    return {
      productList: [],
    }
  },
  created() {
    eventBus.$on("productAdded", (product) => {
      if (this.productList.length < 10) {
        this.productList.push(product);
        eventBus.$emit("progressBarUpdated", this.productList.length);
      } else {
        alert("Daha fazla ürün eklenemez!")
      }
    });
  }
}
</script>