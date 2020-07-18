<template>
  <form class="form-wizard-wrapper">
    <form-wizard color="#FF8A00" ref="wizard">
      <tab-content title="Delivery">
        <div class="wizard-content-wrapper flex">
          <div class="left">
            <div class="flex">
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
                    autocomplete="off"
                    required="required"
                    v-model.trim="$v.email.$model"
                  />
                  <label for="email" class="control-label">Email</label>
                  <img
                    v-if="$v.email.$error"
                    class="icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.email.$invalid"
                    class="icon"
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
                    autocomplete="off"
                    required="required"
                    v-model.trim="$v.phone.$model"
                    @keydown="checkNumber"
                  />
                  <label for="phone" class="control-label">Phone Number</label>
                  <img
                    v-if="$v.phone.$error"
                    class="icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.phone.$invalid"
                    class="icon"
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
                    cols="30"
                    rows="3"
                    required="required"
                    v-model.trim="$v.address.$model"
                    @keyup="remaincharCount()"
                  ></textarea>
                  <label for="address" class="control-label">Delivery Address</label>
                  <span class="note">{{ remaincharactersText }}</span>
                  <img
                    v-if="$v.address.$error"
                    class="icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.address.$invalid"
                    class="icon"
                    src="../assets/images/icon-check.svg"
                    alt="icon"
                  />
                </div>
              </div>
              <div class="flex-item">
                <label class="checkbox">
                  Send as dropshipper
                  <input type="checkbox" id="dropshipper" v-model="isChecked" />
                  <span class="checkmark" for="dropshipper"></span>
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
                    required="required"
                    :disabled="!isChecked"
                    v-model.trim="$v.dropshipperName.$model"
                  />
                  <label for="dropshipper-name" class="control-label">Dropshipper Name</label>
                  <img
                    v-if="$v.dropshipperName.$error"
                    class="icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.dropshipperName.$invalid"
                    class="icon"
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
                    required="required"
                    autocomplete="off"
                    :disabled="!isChecked"
                    v-model.trim="$v.dropshipperPhone.$model"
                    @keydown="checkNumber"
                  />
                  <label for="dropshipper-phone" class="control-label"
                    >Dropshipper Phone Number</label
                  >
                  <img
                    v-if="$v.dropshipperPhone.$error"
                    class="icon"
                    src="../assets/images/icon-clear.svg"
                    alt="icon"
                  />
                  <img
                    v-if="!$v.dropshipperPhone.$invalid"
                    class="icon"
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
                <div class="summary__label">10 items purchased</div>
              </div>
              <div class="flex-item">
                <div class="flex summary-detail">
                  <div class="flex-item">
                    <div class="summary__label">Costs of goods</div>
                    <div class="summary__label">Dropshipping fee</div>
                    <div class="wizard__subtitle">Total</div>
                  </div>
                  <div class="flex-item">
                    <div class="summary__value">{{ costs }}</div>
                    <div class="summary__value">{{ dropshipperFee }}</div>
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
            <form>
              <div></div>
            </form>
            <h2 class="wizard__title">Payment</h2>
            <form></form>
          </div>
          <div class="right">
            <h3 class="wizard__subtitle">Summary</h3>
          </div>
        </div>
      </tab-content>
      <tab-content title="Finish">
        <div class="wizard-content-wrapper flex">
          <div class="left">
            <h2 class="wizard__title">Thank you</h2>
          </div>
          <div class="right">
            <h3 class="wizard__subtitle">Summary</h3>
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
            >Pay with e-Wallet</wizard-button
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
      maxLength: maxLength(120),
    },
  },
  methods: {
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

  .vue-form-wizard
    padding 0

  .wizard-tab-content
    padding 30px 0 0 20px

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
    .wizard__subtitle
      subtitle()
      margin-bottom .5rem
    .left
      flex-basis 73%
      padding-right $padding
      border-right  1px solid $secondary-lighten3
      .flex
        justify-content space-between
        align-items flex-start
        .flex-item
          &:nth-child(odd)
            flex-basis 56%
          &:nth-child(even)
            flex-basis 40%
            text-align right
        .checkbox
          margin: 1.6rem 0 2.6rem;
          display inline-block
    .right
      flex-basis 27%
      padding-left $padding
      .summary
        height 95%
        flex-direction column
        justify-content space-between
      .summary-detail
        justify-content space-between
        .flex-item:last-child
          text-align right
      $margin = 10px
      .summary__label
        color $secondary-lighten2
        margin-bottom $margin
      .summary__value
        font-weight 600
        margin-bottom $margin
</style>
