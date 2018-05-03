<template>
  <div class="hero is-fullheight is-primary is-bold">
    <div class="hero-body">
      <div class="container container-form">
        <h2 class="subtitle is-2 has-text-centered"><i class="fas fa-warehouse"></i></h2>
        <h1 class="title is-1 has-text-centered">Payment Roomie</h1>
        <div class="field">
          <label class="label has-text-white">Roomie #1 incoming $/month</label>
          <p class="control has-icons-left">
            <input type="number" v-model="roomieOneIncoming" class="input">
            <span class="icon is-small is-left">
              <i class="fas fa-user"></i>
            </span>
          </p>
        </div>
        <div class="field">
          <label class="label has-text-white">Roomie #2 incoming $/month</label>
          <p class="control has-icons-left">
            <input type="number" v-model="roomieTwoIncoming" class="input" placeholder="roomie #1 incoming $/month">
            <span class="icon is-small is-left">
              <i class="fas fa-user"></i>
            </span>
          </p>
        </div>
        <div class="field">
          <label class="label has-text-white">Room payment by month</label>
          <p class="control has-icons-left">
            <input type="number" v-model="roomPayment" class="input" placeholder="Room payment by month">
            <span class="icon is-small is-left">
              <i class="fas fa-dollar-sign"></i>
            </span>
          </p>
        </div>
        <div class="field">
          <button class="button is-dark is-fullwidth" @click="calculate">Calculate</button>
        </div>
        <hr>
        <div class="columns">
          <div class="column">
            <div class="field">
              <label class="label has-text-white">Roomie #1 payment</label>
              <p class="control has-icons-left">
                <input type="number" class="input" :value="totalOnePayment" readonly>
                <span class="icon is-small is-left">
                  <i class="fas fa-user"></i>
                </span>
              </p>
            </div>
          </div>
          <div class="column">
            <div class="field">
              <label class="label has-text-white">Roomie #1 percent</label>
              <p class="control has-icons-left">
                <input type="number" class="input" :value="percent" readonly>
                <span class="icon is-small is-left">
                  <i class="fas fa-percent"></i>
                </span>
              </p>
            </div>
          </div>
        </div>
        <div class="columns">
          <div class="column">
            <div class="field">
              <label class="label has-text-white">Roomie #2 payment</label>
              <p class="control has-icons-left">
                <input type="text" class="input" :value="totalTwoPayment" readonly>
                <span class="icon is-small is-left">
                  <i class="fas fa-user"></i>
                </span>
              </p>
            </div>
          </div>
          <div class="column">
            <div class="field">
              <label class="label has-text-white">Roomie #2 percent</label>
              <p class="control has-icons-left">
                <input type="text" class="input" :value="percent" readonly>
                <span class="icon is-small is-left">
                  <i class="fas fa-percent"></i>
                </span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      roomieOneIncoming: 0,
      roomieTwoIncoming: 0,
      roomPayment: 1,
      totalOnePayment: 0,
      totalTwoPayment: 0,
      percent: 0,
    }
  },
  methods: {
    calculate() {
      const roomieOneIncoming = Number.isInteger(parseInt(this.roomieOneIncoming)) ? parseInt(this.roomieOneIncoming) : 0;
      const roomieTwoIncoming = Number.isInteger(parseInt(this.roomieTwoIncoming)) ? parseInt(this.roomieTwoIncoming) : 0;
      const roomPayment = Number.isInteger(parseInt(this.roomPayment)) ? parseInt(this.roomPayment) : 1;
      const percent = (roomPayment * 100)/(roomieOneIncoming + roomieTwoIncoming);
      const totalOne = (percent/100) * roomieOneIncoming;
      const totalTwo = (percent/100) * roomieTwoIncoming;
      
      this.totalOnePayment = parseFloat(totalOne).toFixed(2);
      this.totalTwoPayment = parseFloat(totalTwo).toFixed(2);
      this.percent = parseFloat(percent).toFixed(2);
    }
  }
}
</script>

<style lang="scss">
@import '~bulma/sass/utilities/initial-variables';
$primary: #155B8A;
$family-primary: 'Quicksand', sans-serif;
@import '~bulma';

.container-form {
  max-width: 400px;
}
</style>
