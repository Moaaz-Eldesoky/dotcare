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
            <!-- <Multiselect
              :selected="selected"
              :options="options"
              @update="updateSelected"
            ></Multiselect> -->
          </div>
        </div>
        <div class="d-flex search-button">
          <input
            type="submit"
            class="btn btn-primary"
            value="Search"
            :disabled="
              picked == '' ||
              (picked == 'specific_product' && product_selected == 0)
            "
            @click="(search_result = true), search_excution(),calc_pagination(),goto('r-box')"
          />
        </div>
      </div>
      <div class="container-fluid product-detailes">
        <div class="secondary-header">
          <img src="../static/doc_icon.png" height="20rem" />
          <h4 class="d-inline-block font-weight-bold">Product Detailes</h4>
          <hr />
        </div>
        <div class="search-result" ref="r-box">
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
            <div
              class="row ml-2"
              v-for="item in pagination_arr"
              :key="item.id"
            >
              <div class="col-4 item name">{{ item.name }}</div>
              <div class="col-4 item quantity">{{ item.quantity }}</div>
              <div class="col-4 item type">{{ typeTemp.type }}</div>
            </div>
          </div>
        </div>
        <div class="result_footer d-flex justify-content-between">
          <div class=" pagination_cont">
            <v-pagination v-model="currentPage" :page-count="pagesNum" @change="calc_pagination()"></v-pagination>
          </div>
          <div v-if="search_result==true" class=" text-right">
            <input
            type="submit"
            value="clear"
            class="btn d-inline reset_btn"
            @click="search_result = false"
          />
          </div>
          <div v-if="search_result==false" class=" text-right">
          <p class="">no items to display</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import Multiselect from "vue-multiselect";
import vPagination from 'vue-plain-pagination'
import JsonData from "../static/json/product_store.json";
export default {
  // components: { Multiselect },
  components: { vPagination },
  data: () => {
    return {
      search_result: false,
      json_arr: JsonData,
      // v-model variables
      warehouse_selected: 0,
      type_selected: 0,
      product_selected: 0,
      picked: "",
      show_zero_st: false,
      currentPage: 1,
      // pageCount:0,
      // selected: null,
      // options: ["static", "json", "options", "items"],
      // filterd arrayes
      WH_types_arr: [],
      TY_product_arr: [],
      typeTemp: "",
      final_search_arr: [],
      pagination_arr:[],
      pagesNum:0
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
      this.typeTemp = products_filteration;
      this.TY_product_arr = products_filteration.products;
    },
    product_filter() {
      if (this.picked == "all_products") {
        this.final_search_arr = this.TY_product_arr;
        console.log("hello all products applied successfuly" +this.final_search_arr);
      }
      else if (this.product_selected != 0) {
        let sp_filter = this.TY_product_arr.filter(
          (el) => el.name == this.product_selected
        );
        this.final_search_arr = sp_filter;
        console.log("hello sp_filter applied successfuly");
      }
    },
    // updateSelected(newSelected) {
    //   this.selected = newSelected;
    // },
    check_zero() {
      if (this.show_zero_st == false) {
        let zeroFilter = this.final_search_arr.filter((el) => el.quantity > 0);
        this.final_search_arr = zeroFilter;
        console.log("hello from zero filteration");
        console.log(zeroFilter);
      } else {
        this.final_search_arr;
        console.log("hello non zero filteration final search array is"+this.final_search_arr);
      }
    },
    calc_pagination(){
      this.pagination_arr = this.final_search_arr.slice(this.currentPage * 2 - 2,(this.currentPage * 2 - 2) + 2)         //it returns array of objs >> end object not included
      console.log("pagination array is:"+ this.pagination_arr);
    },
    calc_pages_nums(){
      this.pagesNum = Math.ceil(Object.keys(this.final_search_arr).length/2);
      console.log("pages num is : " + this.pagesNum);
    },
    reset_all() {
      this.warehouse_selected = 0;
      this.type_selected = 0;
      this.product_selected = 0;
      this.picked = "";
      this.show_zero_st = false;
      this.currentPage = 1;
    },
    search_excution() {
      this.product_filter();
      this.check_zero();
      this.calc_pages_nums();
      this.reset_all();
    },
    goto(refName) {
      var element = this.$refs[refName];
      var top = element.offsetTop;
      window.scrollTo(0, top);
    },
  },
  watch: {},
};
</script>

<style>
.pagination ul{
  border: 1px solid red;
  margin-top: 0px;
}
.pagination li button{
  border: 1px solid #DDD;
  background-color: white;
  font-size: 1.5rem;
  font-weight: 600;
  color:black;
  padding: 0rem 1rem;
}
.pagination-link--active{
  background-color: #48dbdf !important;
}
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
.result_footer {
  background-color: #e5eaef;
  margin-right: -15px;
  margin-left: -15px;
  padding-right: 1rem;
  padding-top: 0.15rem;
  font-size: 1.25rem;
  height: 3rem;
}
.reset_btn {
  font-size: 1.25rem;
  padding: 0px;
}
.pagination_cont{
  margin-left: 1rem;
  width:2rem ;
}

</style>

