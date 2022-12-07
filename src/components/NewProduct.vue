<template>
        <div class="row">
      <div class="card offset-2 col-md-3">
        <div class="card-body tex-center d-flex align-items-center flex-column">
          <img height="128" class="img-responsive text-center mb-3"
               :src="product.selectedImage == null ? '/src/assets/4.jpeg' : product.selectedImage">
          <input ref="file" type="file" style="display: none;" @change="onChange($event)" class="form-control">
          <button class="btn btn-outline-secondary " type="button" @click="$refs.file.click()">Resim Seç</button>
        </div>
      </div>
      <div class="col-md-5">
        <div class="col-md-11 card">
          <div class="card-body">
            <div class="form-group">
              <label>Başlık</label>
              <input type="text" v-model="product.title" class="form-control" placeholder="Başlık Giriniz">
            </div>
            <div class="row">
              <div class="form-group col-md-6">
                <label>Resmin Linki</label>
                <input type="text" v-model="product.link" class="form-control" placeholder="Linki Giriniz">
              </div>
            </div>
            <button @click= "addProduct" class="btn btn-outline-info btn-block">Ekle!</button>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import { eventBus } from "../main";

export default {
    data() {
      return {
        product : {
            title: null,
            link: null,
        }
      }
    },
    methods: {
      onChange(e) {
        const file = e.target.files[0];
        this.product.selectedImage = URL.createObjectURL(file);
      },
    addProduct(){
        eventBus.$emit("productAdded", this.product);
        this.product={
            title: null,
            link: null,
        }
        }
    }   
}
</script>