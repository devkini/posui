<template>
    <table class="table">
        <thead>
            <th>Item Name</th>
            <th>Qty</th>
            <th>Price</th>
            <th></th>
        </thead>
        <tbody>
            <tr v-for="order in orders">
                <td>{{ order.name }}</td>
                <td>{{ order.qty }}</td>
                <td>{{ order.total }}</td>
                <td @click="removeOrder(order)"><span class="glyphicon glyphicon-remove" aria-hidden="true"></span></td>
            </tr>
            <tr>
                <td></td>
                <td><b>Total</b></td>
                <td>{{ totalOrder }}</td>
                <td></td>
            </tr>
        </tbody>
    </table>
    <pre v-if="debug">{{ $data | json }}</pre>
</template>

<script>
import _ from 'lodash'

export default {
  props: ['orders', 'debug'],
  computed: {
    totalOrder: function () {
      return _.sumBy(this.orders, 'total')
    }
  },
  methods: {
    removeOrder: function (item) {
      this.orders.$remove(item)
    }
  }
}
</script>
