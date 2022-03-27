<template>
 <div>
  <v-header></v-header>
  <div class="tab">
    <div class="tab-item">商品</div>
    <div class="tab-item">评价</div>
    <div class="tab-item">商家</div>
  </div>
   
  </div>
</template>

<script type="text/ecmascript-6">
  //import {urlParse} from 'common/js/util';
  import header from './components/header/header';

  const ERR_OK = 0;

  export default {
    data() {
      return {
        seller: {
          id: (() => {
            let queryParam = urlParse();
            return queryParam.id;
          })()
        }
      };
    },
    created() {
      this.$http.get('/api/seller?id=' + this.seller.id).then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = Object.assign({}, this.seller, response.data);
        }
      });
    },
    components: {
      'v-header': header
    }
  };

</script>

<style>
body {
  font-family: "微软雅黑";
}
.tab{ display:flex}
</style>
