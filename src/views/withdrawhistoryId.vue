<template>
  <body class="bod" style="background-color: #cccccc">
    <div>
      <div style="display: inline-block">withdraw history</div>
      <h1 class="text-center font-bold leading-10 text-gray-800">
        {{ users }}
      </h1>
      <div class="userId" v-for="order in orders" :key="order._id">
        {{ order.userId }}
      </div>
      <div class="inor">
        <div class="balance">
          <div style="font-weight: 800">amount</div>
          <h1
            v-for="user in orders"
            :key="user._id"
            class="text-center font-bold leading-10 text-gray-800"
          >
            {{ user.amount }}
          </h1>
        </div>
        <div class="profit">
          <div style="font-weight: 800">with tax</div>
          <h1
            v-for="user in orders"
            :key="user._id"
            class="text-center font-bold leading-10 text-gray-800"
          >
            {{ user.prs }}
          </h1>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
import AuthenticationServices from "@/services/AuthenticationServices";

export default {
  name: "MyComponent",
  data() {
    return {
      orders: [],
      users: "",
      id: "",
    };
  },
  async created() {
    this.id = this.$route.params.id;
    const orderId = this.id;
    const response = await AuthenticationServices.getonewithdrawhistory(
      orderId
    );
    this.orders = response.data;
    this.users = response.data.orders.createdAt;
    console.log(this.users);
  },
  methods: {
    copyTestingCode() {
      //   this.$router.push(`/order`);
    },
    async deletedeposit() {
      const orderId = this.id;
      const response = await AuthenticationServices.deletedeposit(orderId);
      console.log(response);
    },
  },
};
</script>

<style scoped>
.bod {
  height: 550px;
}
.userId {
  position: relative !important;
  top: 8px !important;
  font-size: large;
  font-weight: bolder;
}
.inor {
  position: relative !important;
  top: 35px !important;
}
.balance {
  display: inline-block;
  position: relative;
  right: 20%;
}
.profit {
  display: inline-block;
  position: relative;
  left: 20%;
}
</style>
