<template>
  <div class="container-fluid full-page">
    <h3 class="main-header font-weight-bold mt-3 mb-3">Product</h3>
    <div class="border p-4">
      <div class="basic-informaion">
        <div class="secondary-header pt-4">
          <img src="../static/note_icon.png" height="20rem" />
          <h4 class="d-inline-block font-weight-bold">Basic Information</h4>
          <hr />
        </div>
        <div class="row">
          <div class="col">
            <label class="d-block">Warehouse <span>*</span></label>
            <select
              class="form-select"
              id="warehouse"
              v-model="warehouse_selected"
              @change="filteredType"
            >
              <option value="0" selected>Select Warehouse</option>
              <option
                v-for="item in json_arr"
                :value="item.name"
                :key="item.id"
              >
                {{ item.name }}
              </option>
            </select>
          </div>
          <div class="col">
            <label class="d-block">Type <span>*</span></label>
            <select
              class="form-select"
              v-model="type_selected"
              :disabled="warehouse_selected < 1"
              @change="filteredProducts"
            >
              <option value="0" selected>Select Type</option>
              <option
                v-for="item in WH_types_arr"
                :value="item.type"
                :key="item.id"
              >
                {{ item.type }}
              </option>
            </select>
          </div>
          <div class="col pt-5">
            <input
              type="checkbox"
              v-model="show_zero_st"
              :value="show_zero_st"
              :disabled="type_selected < 1"
            />
            <label>Show Zero Balance</label>
          </div>
        </div>
        <div class="row mt-5">
          <div class="col-4">
            <label class="d-block">Product Classification</label>
            <div class="form-check form-check-inline">
              <input
                class="form-check-input"
                type="radio"
                name="flexRadioDefault"
                id="flexRadioDefault1"
                value="all_products"
                :disabled="type_selected < 1"
                v-model="picked"
                checked
              />
              <label class="form-check-label" for="flexRadioDefault1">
                All Products
              </label>
            </div>
            <div class="form-check form-check-inline">
              <input
                class="form-check-input"
                type="radio"
                name="flexRadioDefault"
                id="flexRadioDefault2"
                value="specific_product"
                :disabled="type_selected < 1"
                v-model="picked"
              />
              <label class="form-check-label" for="flexRadioDefault2">
                Spacific Product
              </label>
            </div>
          </div>
          <div class="col-6" v-show="picked == 'specific_product'">
            <label class="d-block">Product <span>*</span></label>
            <select v-model="product_selected" class="form-select">
              <option :value="0" selected>Select Product</option>
              <option
                v-for="item in TY_product_arr"
                :value="item.name"
                :key="item.id"
              >
                {{ item.name }}
              </option>
            </select>
          </div>
        </div>
        <div class="d-flex search-button">
          <input
            type="submit"
            class="btn btn-primary"
            value="Search"
            :disabled="picked == '' || (picked=='specific_product' && product_selected == 0)"
            @click="search_result=true,search_excution()"
          />
        </div>
      </div>
      <div class="container-fluid product-detailes">
        <div class="secondary-header">
          <img src="../static/doc_icon.png" height="20rem" />
          <h4 class="d-inline-block font-weight-bold">Product Detailes</h4>
          <hr />
        </div>
        <div class="search-result">
          <div class="row labels">
            <div class="col-4">Product</div>
            <div class="col-4">On-Hand</div>
            <div class="col-4">Type</div>
          </div>
          <div class="row search-boxes">
            <div class="col-4">
              <form class="search-container">
                <input type="text" id="search-bar" />
                <a href="#">
                  <img class="search-icon" src="../static/search_icon.png" />
                </a>
              </form>
            </div>
            <div class="col-4">
              <form class="search-container">
                <input type="text" id="search-bar" />
                <a href="#">
                  <img class="search-icon" src="../static/search_icon.png" />
                </a>
              </form>
            </div>
            <div class="col-4">
              <form class="search-container">
                <input type="text" id="search-bar" />
                <a href="#">
                  <img class="search-icon" src="../static/search_icon.png" />
                </a>
              </form>
            </div>
          </div>
        </div>
        <!-- ************************ -->
        <div class="result-box">
          <div class="empty-result" v-if="search_result == false">
            <img
              src="../static/health-folder-icon.jpg"
              class="m-auto d-block"
            />
            <p class="text-center">Select Warehouse and Product</p>
          </div>
          <div class="results" v-if="search_result == true">
            <div class="row ml-2" v-for="item in final_search_arr" :key="item.id">
                <div class="col-4 item name">{{ item.name }}</div>
                <div class="col-4 item quantity">{{ item.quantity }}</div>
                <div class="col-4 item type">{{ typeTemp.type }}</div>
            </div>
          </div>
        </div>
        <!-- ***Need to Add Pagnation Component*** -->
        <div class="pagenation">
          <input
            type="submit"
            value="clear"
            class="btn d-inline reset_btn"
            @click="search_result=false">
          <p class="d-inline">no items to display</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import JsonData from "../static/json/product_store.json";
export default {
  data: () => {
    return {
      search_result:false,
      json_arr: JsonData,
      // v-model variables
      warehouse_selected: 0,
      type_selected: 0,
      product_selected: 0,
      picked: "",
      show_zero_st: false,
      // filterd arrayes
      WH_types_arr: [],
      TY_product_arr: [],
      typeTemp:"",
      final_search_arr:[],
    };
  },
  methods: {
    filteredType() {
      let types_filteration = JsonData.find((el) =>
        el.name.includes(this.warehouse_selected)
      );
      this.WH_types_arr = types_filteration.types;
    },
    filteredProducts() {
      let products_filteration = this.WH_types_arr.find((el) =>
        el.type.includes(this.type_selected)
      );
      this.typeTemp=products_filteration;
      this.TY_product_arr = products_filteration.products;
    },
    product_filter(){
      if(this.picked=="all_products"){
        this.final_search_arr=this.TY_product_arr;
        console.log("hello all products applied successfuly")
      }
      else if (this.product_selected != 0){
        let sp_filter = this.TY_product_arr.filter((el) => el.name == this.product_selected);
        this.final_search_arr=sp_filter;
        console.log("hello sp_filter applied successfuly")
      }
    },
    check_zero(){
      if (this.show_zero_st == false) {
        let zeroFilter = this.final_search_arr.filter((el) => el.quantity > 0);
        this.final_search_arr = zeroFilter;
        console.log("hello from zero filteration")
        console.log(zeroFilter);
      }
      else{
        this.final_search_arr;
        console.log("hello non zero filteration")
        console.log(this.final_search_arr);
      }
    },
    reset_all(){
      this.warehouse_selected= 0
      this.type_selected= 0
      this.product_selected= 0
      this.picked= ""
      this.show_zero_st= false
    },
    search_excution(){
      this.product_filter();
      this.check_zero();
      this.reset_all();
    },

  },
  watch: {

  }
};
</script>

<style scoped>
.border {
  margin-bottom: 5rem;
  background-color: #fff;
}
.secondary-header {
  font-size: 1.3rem;
}
.basic-informaion label {
  color: gray;
}
.basic-informaion label span {
  color: red;
}
.form-select {
  font-size: 1.5rem;
  padding: 0.5rem;
  width: 80%;
  background-color: #e8e5e5;
}
.form-check .form-check-label {
  font-size: 1.3rem;
}
.search-button {
  justify-content: flex-end;
}
.search-button input {
  background-color: #48dbdf;
  color: white;
  border: none;
  padding: 0.6rem;
  font-size: 1.5rem;
  width: 10rem;
}
/* search style start*/
.search-container {
  position: relative;
}
#search-bar {
  width: 100%;
  height: 2.5rem;
  border: 1px solid #ddd;
}
#search-bar:focus {
  border: none;
}
.search-icon {
  position: absolute;
  height: 2rem;
  right: 1rem;
  top: 00.5rem;
}
.labels {
  background-color: #b0cbe7;
}
.search-boxes {
  background-color: #e2e9ef;
  padding-top: 00.5rem;
  padding-bottom: 00.5rem;
}

.result-box {
  height: 30rem;
  border: 1px solid #ddd;
  margin-right: -15px;
  margin-left: -15px;
  padding-top: 2rem;
}
.result-box img {
  height: 20rem;
}
.pagenation {
  background-color: #e5eaef;
  margin-right: -15px;
  margin-left: -15px;
  padding-right: 1rem;
  padding-top: 0.5rem;
  font-size: 1.25rem;
  height: 3rem;
}
.pagenation p{
  float: right;
}
.reset_btn{
  font-size: 1.25rem;
  padding: 0px;
  margin-left: 1rem;
}
</style>

