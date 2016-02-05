<template>
<div class="row" id="app">
    <div class="col-md-4">
        <div class="panel panel-primary">
            <div class="panel-heading">
                Order Items
            </div>
            <div class="panel-body">
                <checkout :orders="orders" :debug="debug"></checkout>
            </div>
        </div>
    </div>
    <div class="col-md-8">
      <div class="panel panel-info">
           <div class="panel-heading">
              Select Items
          </div>
          <div class="panel-body">
              <div class="row">
                  <form>
                      <div class="form-group">
                          <input type="text" class="form-control" placeholder="Search Items" v-model="search">
                      </div>
                  </form>
              </div>
              <div class="row">
                  <div class="col-md-2" v-for="item in items | filterBy search">
                      <div class="col-md-2" @click="addOrder(item)">{{ item.name }}</div>
                  </div>
              </div>
          </div>
          <div class="panel-footer">Panel footer</div>
      </div>
      <!-- debugging -->
      <input type="checkbox" v-model="debug" /> Enable Debug
      <pre v-if="debug">{{ $data | json }}</pre>
      <br />
      <span>Source code - <a href="https://github.com/devkini/posui">https://github.com/devkini/posui</a></span>
    </div>
</div>
</template>

<script>
import _ from 'lodash'
import Checkout from './components/Checkout'

export default {
  components: {
    Checkout
  },
  data () {
    return {
      showRight: false,
      orders: [],
      items2: ['item 1', 'item 2'],
      items: [
        { name: 'Item-1', barcode: _.uniqueId('bar'), price: 15},
        { name: 'Item-2', barcode: _.uniqueId('bar'), price: 5},
        { name: 'Item-3', barcode: _.uniqueId('bar'), price: 11},
        { name: 'Item-4', barcode: _.uniqueId('bar'), price: 10},
        { name: 'Item-5', barcode: _.uniqueId('bar'), price: 15},
        { name: 'Item-6', barcode: _.uniqueId('bar'), price: 5},
        { name: 'Item-7', barcode: _.uniqueId('bar'), price: 11},
        { name: 'Item-8', barcode: _.uniqueId('bar'), price: 10},
        { name: 'Item-9', barcode: _.uniqueId('bar'), price: 10},
        { name: 'Item-10', barcode: _.uniqueId('bar'), price: 10}
      ],
      search: '',
      debug: false
    }
  },
  methods: {
    addOrder: function (item) {
      var order
      var quantity = 1

      order = _.find(this.orders, {name: item.name})

      if (order) {
        quantity = order.qty++
      } else {
        order = {name: item.name, price: item.price, qty: quantity, total: item.price}
        this.orders.push(order)
      }

      order.total = order.price * order.qty
    }
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
