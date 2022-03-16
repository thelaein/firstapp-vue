<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8">
          <h3>Voucher : {{vId}}</h3>
          <form @submit.prevent="saveItem">
            <div class="row align-items-end">
              <div class="col">
                   <label for="" class="form-label">Select Item</label>
                  <select class="form-select" v-model="seletedItem">
                    <option v-for="item in items" :value="item.id">{{item.name}}</option>
                  </select>
              </div>
              <div class="col">
                <label for="" class="form-label">Quantity</label>
                <input type="number" class="form-control" v-model="inputQuantity">
              </div>
            
        <div class="col">
          <button class="btn btn-primary">Add</button>
        </div>
            </div>
          </form>
          <table class="table table-bordered my-3" v-if="getListTotal > 0">
            <thead>
              <tr>
              <th>#</th>
              <th>Item</th>
              <th>Quantity</th>
              <th>Uni Price</th>
              <th>Cost</th> 
              </tr>       
            </thead>
            <tbody>
              <tr v-for="(list,index) in lists" :key="index">
                <td>{{index+1}}</td>
                <td>{{list.name}}</td>
                <td>{{list.quantity}}</td>
                <td>{{list.unitPrice}}</td>
                <td>{{list.cost}}</td>
              </tr>
            </tbody>
            <tfoot>
              <tr class="">
                <td>Cost Total</td>
                <td>{{getCostTotal}}</td>
              </tr>
            </tfoot>
          </table>
        </div>
    
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
       vId : (Math.random()*10000).toFixed(0),
      seletedItem : null,
      inputQuantity : null,
      lists : [],
       items : [
         {
           id : 1,
           name: 'apple',
           price:50,
         },
         {
           id : 2,
           name: 'banana',
           price:50,
         },
         {
           id : 3,
           name: 'orange',
           price:50,
         },
       ]
      }
    },
    computed: {
      getListTotal(){
        return this.lists.length
      },
      getCostTotal() {
        return this.lists.reduce((x,y)=> x+y.cost,0)
      }
    },
    methods: {
      saveItem() {
        let list = {
          itemId : this.seletedItem,
          name : this.items.find(el=>el.id === this.seletedItem).name,
          quantity : this.inputQuantity,
          unitPrice : this.items.find(el=>el.id === this.seletedItem).price,
          cost : this.items.find(el=>el.id === this.seletedItem).price * this.inputQuantity
        }

        this.seletedItem = null;
        this.inputQuantity = null;
        this.lists.push(list)
        // alert('Hello')
      }
    },
    
  }
</script>

<style lang="scss" scoped>

</style>