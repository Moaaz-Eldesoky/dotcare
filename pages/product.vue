<template>
  <div class="container-fluid full-page" id="product-container">
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
            <label class="d-block">Warehouse<span>*</span></label>
            <select
              class="form-select"
              id="warehouse"
              @change="
                ($event) =>
                  $event.target.options.selectedIndex != 0
                    ? ((type = false), (balance = false))
                    : ((type = true), (balance = true))
              "
            >
              <option value="0" selected>Select Warehouse</option>
              <option value="1">Warehouse 1</option>
              <option value="2">Warehouse 2</option>
              <option value="3">Warehouse 3</option>
              <option value="4">Warehouse 4</option>
            </select>
          </div>
          <div class="col">
            <label class="d-block">Type <span>*</span></label>
            <select class="form-select" :disabled="type"
            @change="
                ($event) =>
                  $event.target.options.selectedIndex != 0
                    ? ((allProducts = false), (specificProduct = false))
                    : ((allProducts = true), (specificProduct = true))                  
              "
            >
              <option selected>Select Type</option>
              <option value="1">Type A</option>
              <option value="2">Type B</option>
              <option value="3">Type C</option>
            </select>
          </div>
          <div class="col pt-5">
            <input
              type="checkbox"
              :disabled="balance"
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
                value="0"
                :disabled="allProducts"
                @change="
                ($event) =>
                  $event.target.checked != 0
                    ? product = true
                    : product = false
              "
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
                value="1"
                :disabled="specificProduct"
                @change="
                ($event) =>
                  $event.target.checked != 0
                    ? product = false
                    : product = true
              "
              />
              <label class="form-check-label" for="flexRadioDefault2">
                Spacific Product
              </label>
            </div>
          </div>
          <div class="col-6" v-if="product==false">
            <label class="d-block">Product<span>*</span></label>
            <select class="form-select" :disabled="product">
              <option selected>Product 1</option>
              <option value="1">Product 2</option>
              <option value="2">Product 3</option>
              <option value="3">Product 4</option>
            </select>
          </div>
        </div>
        <div class="d-flex search-button">
          <input type="submit" class="btn btn-primary" value="Search" @click="search_toggeler=!search_toggeler" />
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
          <div class="empty-result" v-if="search_toggeler==true">
            <img
            src="../static/health-folder-icon-2.jpg"
            class="m-auto d-block"
          />
          <p class="text-center">Select Warehouse and Product</p>
          </div>
          <div class="results "  v-if="search_toggeler==false">
            <div class="row ml-2"  v-for="item in productsData" :key="item.id">
              <div class="col-4 item name">{{item.productName}}</div>
              <div class="col-4 item quantity">{{item.balance}}</div>
              <div class="col-4 item type">{{item.type}}</div>
            </div>
          </div>
        </div>
        <!-- ***Need to Add Pagnation Component*** -->
        <div class="pagenation">
          <p class="text-right">no items to display</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import JsonData from "../static/json/product_store.json"
export default {
  data: () => {
    return {
      type: true,
      balance: true,
      allProducts: true,
      specificProduct: true,
      product: true,
      productsData: JsonData,
      search_toggeler:true,
    };
  },
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
</style>