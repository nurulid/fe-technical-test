<template>
  <form class="form-wizard-wrapper">
    <form-wizard color="#FF8A00" ref="wizard">
      <tab-content title="Delivery">
        <div class="wizard-content-wrapper flex">
          <div class="left">
            <div class="flex delivery">
              <div class="flex-item">
                <h2 class="wizard__title">Delivery details</h2>
                <div
                  class="form-group"
                  :class="[
                    { 'form-group--invalid': $v.email.$error },
                    { 'form-group--valid': !$v.email.$invalid },
                  ]"
                >
                  <input
                    type="email"
                    name="email"
                    id="email"
                    class="form-group__input"
                    autocomplete="off"
                    required="required"
                    v-model.trim="$v.email.$model"
                  />
                  <label for="email" class="form-group__label">Email</label>
                  <img
                    v-if="$v.email.$error"
                    class="form-group__icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.email.$invalid"
                    class="form-group__icon"
                    src="../assets/images/icon-check.svg"
                    alt="icon"
                  />
                </div>
                <div
                  class="form-group"
                  :class="[
                    { 'form-group--invalid': $v.phone.$error },
                    { 'form-group--valid': !$v.phone.$invalid },
                  ]"
                >
                  <input
                    type="number"
                    name="phone"
                    id="phone"
                    class="form-group__input"
                    autocomplete="off"
                    required="required"
                    v-model.trim="$v.phone.$model"
                    @keydown="checkNumber"
                  />
                  <label for="phone" class="form-group__label">Phone Number</label>
                  <img
                    v-if="$v.phone.$error"
                    class="form-group__icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.phone.$invalid"
                    class="form-group__icon"
                    src="../assets/images/icon-check.svg"
                    alt="icon"
                  />
                </div>
                <div
                  class="form-group form-group--textarea"
                  :class="[
                    { 'form-group--invalid': $v.address.$error },
                    { 'form-group--valid': !$v.address.$invalid },
                  ]"
                >
                  <textarea
                    name="address"
                    id="address"
                    class="form-group__textarea"
                    cols="30"
                    rows="3"
                    required="required"
                    v-model.trim="$v.address.$model"
                    @keyup="remaincharCount()"
                  ></textarea>
                  <label for="address" class="form-group__label">Delivery Address</label>
                  <span class="form-group__note">{{ remaincharactersText }}</span>
                  <img
                    v-if="$v.address.$error"
                    class="form-group__icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.address.$invalid"
                    class="form-group__icon"
                    src="../assets/images/icon-check.svg"
                    alt="icon"
                  />
                </div>
              </div>
              <div class="flex-item">
                <label class="checkbox">
                  Send as dropshipper
                  <input type="checkbox" id="dropshipper" class="checkbox__input" v-model="isChecked" />
                  <span class="checkbox__checkmark" for="dropshipper"></span>
                </label>
                <div
                  class="form-group"
                  :class="[
                    { 'form-group--invalid': $v.dropshipperName.$error },
                    { 'form-group--valid': !$v.dropshipperName.$invalid },
                  ]"
                >
                  <input
                    type="text"
                    name="name"
                    autocomplete="off"
                    id="dropshipper-name"
                    class="form-group__input"
                    required="required"
                    :disabled="!isChecked"
                    v-model.trim="$v.dropshipperName.$model"
                  />
                  <label for="dropshipper-name" class="form-group__label">Dropshipper Name</label>
                  <img
                    v-if="$v.dropshipperName.$error"
                    class="form-group__icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.dropshipperName.$invalid"
                    class="form-group__icon"
                    src="../assets/images/icon-check.svg"
                    alt="icon"
                  />
                </div>
                <div
                  class="form-group"
                  :class="[
                    { 'form-group--invalid': $v.dropshipperPhone.$error },
                    { 'form-group--valid': !$v.dropshipperPhone.$invalid },
                  ]"
                >
                  <input
                    type="number"
                    name="phone"
                    id="dropshipper-phone"
                    class="form-group__input"
                    required="required"
                    autocomplete="off"
                    :disabled="!isChecked"
                    v-model.trim="$v.dropshipperPhone.$model"
                    @keydown="checkNumber"
                  />
                  <label for="dropshipper-phone" class="form-group__label"
                    >Dropshipper Phone Number</label
                  >
                  <img
                    v-if="$v.dropshipperPhone.$error"
                    class="form-group__icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.dropshipperPhone.$invalid"
                    class="form-group__icon"
                    src="../assets/images/icon-check.svg"
                    alt="icon"
                  />
                </div>
              </div>
            </div>
          </div>
          <div class="right">
            <div class="flex summary">
              <div class="flex-item">
                <h3 class="wizard__subtitle">Summary</h3>
                <div class="label-secondary-lighten">10 items purchased</div>
              </div>
              <div class="flex-item">
                <div class="flex summary-detail">
                  <div class="flex-item">
                    <div class="summary-detail__label">Costs of goods</div>
                    <div class="summary-detail__label">Dropshipping fee</div>
                    <div class="wizard__subtitle">Total</div>
                  </div>
                  <div class="flex-item">
                    <div class="summary-detail__value">{{ costs }}</div>
                    <div class="summary-detail__value">{{ dropshipperFee }}</div>
                    <div class="wizard__subtitle">{{ totalSemua }}</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </tab-content>
      <tab-content title="Payment">
        <div class="wizard-content-wrapper flex">
          <div class="left">
            <h2 class="wizard__title">Shipment</h2>
            <div class="shipment-list">
              <div class="radio-box" v-for="(item, i) in shipment" :key="i">
                <input
                  type="radio"
                  name="shipment"
                  class="radio-box__input"
                  :id="'shipment-' + i"
                  :value="i"
                  v-model="selectedShipment"
                />
                <label class="radio-box__box" :for="'shipment-' + i"></label>
                <div class="radio-box__title">{{ item.name }}</div>
                <div class="radio-box__subtitle">{{ item.cost }}</div>
                <img class="radio-box__icon" src="../assets/images/icon-check.svg" alt="icon check" />
              </div>
            </div>
            <h2 class="wizard__title">Payment</h2>
            <div class="payment-list">
              <div class="radio-box" v-for="(item, i) in payment" :key="i">
                <input
                  type="radio"
                  name="payment"
                  class="radio-box__input"
                  :id="'payment-' + i"
                  :value="item.name"
                  v-model="selectedPayment"
                />
                <label class="radio-box__box" :for="'payment-' + i"></label>
                <div class="radio-box__title">{{ item.name }}</div>
                <div class="radio-box__subtitle"></div>
                <img class="radio-box__icon" src="../assets/images/icon-check.svg" alt="icon check" />
              </div>
            </div>
          </div>
          <div class="right">
            <div class="flex summary">
              <div class="flex-item">
                <h3 class="wizard__subtitle">Summary</h3>
                <div class="label-secondary-lighten">10 items purchased</div>
                <hr>
                <div class="label-secondary">Delivery estimation</div>
                <div class="label-accent">
                  <span class="lowercase">{{ shipment[selectedShipment].deliveryEstimate }}</span> by
                  {{ shipment[selectedShipment].name }}
                </div>
              </div>
              <div class="flex-item">
                <div class="flex summary-detail">
                  <div class="flex-item">
                    <div class="summary-detail__label">Costs of goods</div>
                    <div class="summary-detail__label">Dropshipping fee</div>
                    <div class="summary-detail__label">
                      <strong>{{ shipment[selectedShipment].name }}</strong> shipment
                    </div>
                    <div class="wizard__subtitle">Total</div>
                  </div>
                  <div class="flex-item">
                    <div class="summary-detail__value">{{ costs }}</div>
                    <div class="summary-detail__value">{{ dropshipperFee }}</div>
                    <div class="summary-detail__value">{{ shipment[selectedShipment].cost + 0 }}</div>
                    <div class="wizard__subtitle">
                      {{ totalSemua + shipment[selectedShipment].cost }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </tab-content>
      <tab-content title="Finish">
        <div class="wizard-content-wrapper flex">
          <div class="left">
            <div class="flex finish">
              <h2 class="wizard__title">Thank you</h2>
              <div class="label-secondary">
                Order ID: <span class="uppercase">{{ randomID() }}</span>
              </div>
              <div class="label-secondary-lighten">
                Your order will be delivered
                <span class="lowercase">{{ shipment[selectedShipment].deliveryEstimate }}</span> by
                {{ shipment[selectedShipment].name }}
              </div>
            </div>
          </div>
          <div class="right">
            <div class="flex summary">
              <div class="flex-item">
                <h3 class="wizard__subtitle">Summary</h3>
                <div class="label-secondary-lighten">10 items purchased</div>
                <hr />
                <div class="label-secondary">Delivery estimation</div>
                <div class="label-accent">
                  <span class="lowercase">{{ shipment[selectedShipment].deliveryEstimate }}</span> by
                  {{ shipment[selectedShipment].name }}
                </div>
                <hr />
                <div class="label-secondary">Payment method</div>
                <div class="label-accent">
                  {{ selectedPayment }}
                </div>
              </div>
              <div class="flex-item">
                <div class="flex summary-detail">
                  <div class="flex-item">
                    <div class="summary-detail__label">Costs of goods</div>
                    <div class="summary-detail__label">Dropshipping fee</div>
                    <div class="summary-detail__label">
                      <strong>{{ shipment[selectedShipment].name }}</strong> shipment
                    </div>
                    <div class="wizard__subtitle">Total</div>
                  </div>
                  <div class="flex-item">
                    <div class="summary-detail__value">{{ costs }}</div>
                    <div class="summary-detail__value">{{ dropshipperFee }}</div>
                    <div class="summary-detail__value">{{ shipment[selectedShipment].cost + 0 }}</div>
                    <div class="wizard__subtitle">
                      {{ totalSemua + shipment[selectedShipment].cost }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </tab-content>
      <!-- wizard footer -->
      <template slot="footer" scope="props">
        <div class="wizard-footer-left wizard-footer-left--top">
          <wizard-button v-if="props.activeTabIndex == 0" class="wizard-btn--back"
            >Back to cart</wizard-button
          >

          <wizard-button
            v-if="props.activeTabIndex == 1"
            @click.native="props.prevTab()"
            class="wizard-btn--back"
            >Back to delivery</wizard-button
          >
        </div>
        <div class="wizard-footer-left">
          <wizard-button
            v-if="props.isLastStep"
            @click.native="$refs.wizard.reset()"
            class="wizard-btn--back wizard-btn--center"
            >Go to homepage</wizard-button
          >
        </div>
        <div class="wizard-footer-right">
          <wizard-button
            v-if="props.activeTabIndex == 0"
            @click.native="props.nextTab()"
            class="wizard-footer-right"
            :style="props.fillButtonStyle"
            >Continue to Payment</wizard-button
          >

          <wizard-button
            v-if="props.activeTabIndex == 1"
            @click.native="props.nextTab()"
            class="wizard-footer-right"
            :style="props.fillButtonStyle"
            :disabled="!selectedPayment"
            >Pay with {{ selectedPayment }}</wizard-button
          >
        </div>
      </template>
    </form-wizard>
  </form>
</template>

<script>
import Vue from "vue";
import { FormWizard, TabContent, WizardButton } from "vue-form-wizard";
import "vue-form-wizard/dist/vue-form-wizard.min.css";
import Vuelidate from "vuelidate";
import { required, minLength, maxLength, email } from "vuelidate/lib/validators";

Vue.use(Vuelidate);

var invalidChars = [".", "e"];

export default {
  /* eslint-disable */
  name: "Checkout",
  components: {
    FormWizard,
    TabContent,
    WizardButton,
  },
  data() {
    return {
      isChecked: false,
      phone: null,
      dropshipperPhone: null,
      email: "",
      dropshipperName: "",
      costs: 500000,
      dropshipper: 0,
      total: 0,
      address: "",
      maxcharacter: 120,
      remaincharactersText: "Remaining 120 characters.",
      shipment: [
        {
          name: "GO-SEND",
          cost: 15000,
          deliveryEstimate: "Today",
        },
        {
          name: "JNE",
          cost: 9000,
          deliveryEstimate: "2 Days",
        },
        {
          name: "Personal Courier",
          cost: 29000,
          deliveryEstimate: "1 Day",
        },
      ],
      payment: [
        {
          name: "e-Wallet",
        },
        {
          name: "Bank Transfer",
        },
        {
          name: "Vitual Account",
        },
      ],
      selectedShipment: 0,
      selectedPayment: "",
      genericID: "",
    };
  },
  validations: {
    phone: {
      required,
      minLength: minLength(6),
      maxLength: maxLength(20),
    },
    dropshipperPhone: {
      required,
      minLength: minLength(6),
      maxLength: maxLength(20),
    },
    email: {
      required,
      email: email,
    },
    dropshipperName: {
      required,
      minLength: minLength(1),
    },
    address: {
      required,
      minLength: minLength(10),
      maxLength: maxLength(120),
    },
  },
  methods: {
    randomID() {
      return Math.random()
        .toString(36)
        .substr(2, 5);
    },
    isLastStep() {
      if (this.$refs.wizard) {
        return this.$refs.wizard.isLastStep;
      }
      return false;
    },
    checkNumber(e) {
      if (invalidChars.includes(e.key)) {
        e.preventDefault();
      }
    },
    remaincharCount() {
      if (this.address.length > this.maxcharacter) {
        this.remaincharactersText = `Exceeded ${this.maxcharacter} characters limit.`;
        document.get;
      } else {
        var remainCharacters = this.maxcharacter - this.address.length;
        this.remaincharactersText = `Remaining ${remainCharacters} characters.`;
      }
    },
  },
  computed: {
    dropshipperFee() {
      if (this.isChecked) {
        return (this.dropshipper = 5900);
      } else {
        return (this.dropshipper = 0);
      }
    },
    totalSemua() {
      return this.costs + this.dropshipperFee;
    },
  },
};
</script>

<style lang="stylus">
@import '../assets/stylus/global.styl'
@import '../assets/stylus/vue-form-wizard.styl'

.form-wizard-wrapper
  position relative
  background white
  padding 25px
  margin 50px
  box-shadow 2px 10px 20px rgba(255, 138, 0, 0.1)
  border-radius 4px
  @media small
    margin 50px 10px

  .vue-form-wizard
    padding 0

  .wizard-tab-content
    padding 30px 0 0 20px
    @media medium
      padding-left 0
    @media x-medium
      margin-top 30px

  .wizard-btn
    border-radius 0
    padding 15px 20px
    font-weight normal

  .wizard-footer-left .wizard-btn
    color $secondary-lighten1

  .wizard-footer-left--top
    position absolute
    top 30px
    left  35px
    @media medium
      left 20px
    @media x-medium
      top 54px

  .wizard-btn--back.wizard-btn--center
    position: absolute;
    bottom: 32%;
    left: 19%;
    @media medium
      bottom unset
      top: 32%;
      left: 25%;

  .wizard-btn--back
    position relative
    padding 6px 12px 6px 28px
    text-align left
    &:after
      content ""
      background url('../assets/images/icon-arrow_back.svg') no-repeat
      background-position center center
      position absolute
      top 5px
      left 5px
      width 20px
      height 20px

  .wizard-content-wrapper
    $padding = 25px
    justify-content space-between
    min-height: 400px;
    @media medium
      flex-direction column
    .wizard__title
      title()
      position relative
      display inline-block
      &:after
        content: "";
        width: 115%;
        height: 7px;
        background-color: $secondary-lighten4;
        position: absolute;
        left: 0;
        bottom: 2px;
        z-index: -1;
        @media x-small
          width 100%
    .wizard__subtitle
      subtitle()
      margin-bottom .5rem
    .left
      flex-basis 70%
      padding-right $padding
      border-right  1px solid $secondary-lighten3
      @media large
        flex-basis 65%
      @media medium
        padding-right 0
        border none
      .flex
        justify-content space-between
        align-items flex-start
        @media x-medium
          flex-direction column
        &.delivery
          .flex-item
            &:nth-child(1)
              flex-basis 56%
            &:nth-child(2)
              flex-basis 40%
              text-align right
              @media x-medium
                width 100%
        .checkbox
          margin 1.6rem 0 2.8rem
          display inline-block
      .shipment-list
        margin-bottom 3rem
      .finish
        flex-direction column
        height 70%
        justify-content center
        width 50%
        margin 0 auto
    .right
      flex-basis 30%
      padding-left $padding        
      @media large
        flex-basis 35%        
      @media medium
        padding-left 0
      .summary
        height 100%
        flex-direction column
        justify-content space-between
        > .flex-item
          margin-bottom 40px
      .summary-detail
        justify-content space-between
        .flex-item:last-child
          text-align right
        $margin = 10px
        &__label
          color $secondary-lighten2
          margin-bottom $margin
        &__value
          font-weight 600
          margin-bottom $margin
      hr
        border 1px solid $secondary-lighten4
        margin 1rem 0
        width 35%
</style>
