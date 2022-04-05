<template>
  <div class="container-fluid">
    <h1 class="main-header">Product</h1>
    <div class="container main-form">
      <div class="secondary-header">
        <img src="../static/note_icon.png" height="20rem" />
        <h4 class="d-inline-block font-weight-bold">Basic Information</h4>
        <hr />
      </div>
      <div class="row">
        <div class="col">
          <label class="d-block">Warehouse<span>*</span></label>
          <select class="form-select">
            <option selected>Warehouse 1</option>
            <option value="1">Warehouse 2</option>
            <option value="2">Warehouse 3</option>
            <option value="3">Warehouse 4</option>
          </select>
        </div>
        <div class="col">
          <label class="d-block">Type<span>*</span></label>
          <select class="form-select">
            <option selected>Type A</option>
            <option value="1">Type B</option>
            <option value="2">Type C</option>
            <option value="3">Type D</option>
          </select>
        </div>
        <div class="col pt-5">
          <input type="checkbox" />
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
            />
            <label class="form-check-label" for="flexRadioDefault1">
              Al Products
            </label>
          </div>
          <div class="form-check form-check-inline">
            <input
              class="form-check-input"
              type="radio"
              name="flexRadioDefault"
              id="flexRadioDefault2"
              checked
            />
            <label class="form-check-label" for="flexRadioDefault2">
              Spacific Product
            </label>
          </div>
        </div>
        <div class="col-6">
          <label class="d-block">Product<span>*</span></label>
          <select class="form-select">
            <option selected>Product 1</option>
            <option value="1">Product 2</option>
            <option value="2">Product 3</option>
            <option value="3">Product 4</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.main-form label {
  color: gray;
}
.main-form label span {
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
</style>