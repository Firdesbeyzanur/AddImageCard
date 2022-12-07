<template>
    <div v-if="productList.length > 0">
        <h3 class="text-center">Eklenen Ürünlerin Listesi</h3>
        <hr>
       <div class="row product-container">
        <appProduct v-for="(product, list) in productList" :key="list">
            <img class="card-img-top" 
            width="200px"
            height="250px"
            :src="product.selectedImage" :alt="product.title">
        <div class="card-body">
          <h6 class="card-title">Başlık: {{ product.title }}</h6>
          <small><strong>Link : </strong> <a :href="product.link">{{ product.link }}</a> </small>
        </div>
        </appProduct>
    </div>
</div>
</template>

<script>
import { eventBus } from "../main";
import Product from "./Product";
export default{
    components: {
        appProduct: Product
    },
    data(){
        return{
            productList: [],
        }
    },
    created(){
        eventBus.$on("productAdded", (product) => { if(this.productList.length < 10 ){
            this.productList.push(product);
            eventBus.$emit("progressBarUpdated", this.productList.length);
        } 
        else {
            alert("Daha fazla resim ve link ekleyemezsiniz !!!")
        }
        });
    }
}
</script>
