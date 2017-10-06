<template>
  <b-container>
    <b-row align-h="center">
      <b-col sm="5">
        <b-card header="Кредитный калькулятор">
          <b-form>
            <b-form-group id="loan-value-group" label="Сумма займа:" label-for="loan-value">
              <b-input id="loan-value-txt" type="number" v-model="loanValue" step="1000" min="1000" max="35000" required></b-input>
              <b-input id="loan-value-rng" type="range" v-model="loanValue" step="1000" min="1000" max="35000"></b-input>
            </b-form-group>
            <b-form-group id="loan-days-group" label="Срок займа:" label-for="loan-days">
              <b-input id="loan-days-txt" type="number" v-model="loanDays" min="5" required></b-input>
              <b-input id="loan-days-rng" type="range" v-model="loanDays" min="5" max="365"></b-input>
            </b-form-group>
          </b-form>
          <div slot="footer">
            <b-form-group id="loan-payback-value-group" label="Сумма к возврату:">
              <span class="text-success">{{ loanPaybackValue }}</span>
            </b-form-group>
            <b-form-group id="loan-payback-date-group" label="Дата возврата займа:">
              <span class="text-dark">{{ loanPaybackDate }}</span>
            </b-form-group>
          </div>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
  import moment from 'moment'
  moment.locale('ru')

  const loanInterest = function (value, days) {
    return Number(value) + (Number(value) * Number(days) * 0.00135)
  }

  export default {
    name: 'calculator',
    data () {
      return {
        loanValue: 0,
        loanDays: 0
      }
    },
    computed: {
      loanPaybackValue () {
        return loanInterest(this.loanValue, this.loanDays)
      },
      loanPaybackDate () {
        return moment().add(this.loanDays, 'days').format('DD MMMM YYYY')
      }
    }
  }
</script>

