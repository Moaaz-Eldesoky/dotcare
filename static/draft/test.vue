<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  setup() {

  },


// 1 >> 1 >> currentPage * 8 - 7

              // 2 >> 9 >> 2*8 - 7
              // 3 >> 17 >> 3*8 - 7






  if (this.picked == "all_products") {
        let pagination_array = [];
        for (let i = this.currentPage * 2 - 1; i < (this.currentPage * 2 - 1) + 2; i++) {
          pagination_array = this.TY_product_arr[i];
        }
        console.log("pagination is" + pagination_array  )
        this.final_search_arr = pagination_array;
})














</script>
