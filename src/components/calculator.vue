<template>
 <b-container fluid>
    <b-row align-h="center">
      <b-col sm="7" md="6" lg="4" xl="4" cols="10">
        <b-card header="<h5>Кредитный калькулятор</h5>">
          <b-form>
            <b-form-group id="loan-value-group" label="Сумма займа:" label-for="loan-value">
             <b-input-group right="руб.">
    <b-input id="loan-value-txt" type="number" v-model="loanValue" step="1000" min="1000" max="35000" required @blur.native="formatValue(loanValue, $event)"></b-input>
  </b-input-group>
              
              <b-input id="loan-value-rng" type="range" v-model="loanValue" step="1000" min="1000" max="35000"></b-input>
            </b-form-group>
            <b-form-group id="loan-days-group" label="Срок займа:" label-for="loan-days">
            <b-input-group right="дней">
              <b-input id="loan-days-txt" type="number" v-model="loanDays" min="5" required @blur.native="formatDate(loanDays, $event)"></b-input>
              </b-input-group>
              <b-input id="loan-days-rng" type="range" v-model="loanDays" min="5" max="365"></b-input>
            </b-form-group>
          </b-form>
          <template slot="footer" class="">
            <p class="m-0">
            Сумма к возврату:
            </p>
              <p class="result-text payback-value text-success">{{ loanPaybackValue }}</p>           
              <p class="m-0 ">
            Дата возврата займа:
            </p>            
              <p class="result-text">{{ loanPaybackDate }}</p>
          </template>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
  import moment from 'moment'
  moment.locale('ru')

  const loanInterest = function (value, days) {
	let valInt = Number(value)
  let daysInt = Number(days)
    return (valInt + (valInt * daysInt * 0.00135)).toFixed(2)
  }

  export default {
    name: 'calculator',
     data () {
      return {
        loanValue: '0',
        loanDays: '0',
      }
    },
    computed: {
      loanPaybackValue () {
        return loanInterest(this.loanValue, this.loanDays)
      },
      loanPaybackDate () {
        return moment().add(this.loanDays, 'days').format('DD MMMM YYYY')
      }
    },
    watch: {
    loanValue (newVal, oldVal) {
       if (!(newVal %1000)) {       
        this.state = 1
       }
    }
    },
    methods: {
       formatValue(value, event) {
        return this.loanValue = Math.ceil(value / 1000)*1000;
      },
			formatDate(value, event) {
       if (value < 5) value = 5
       return this.loanDays = value
      }
    }
  }
</script>

<style>
* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  padding: 20px;
  height: 350px;
  min-width: 410px;
}

.card {
  box-shadow: 0 0 10px rgba(0,0,0,0.3);
}

.card-header {
  text-align:center;
}

.input-data {
  font-weight: bold;
  font-size: 1.5em;
  text-align:center;
  text-decoration: underline;
}

.result-text {
  font-weight: bold;
  font-size: 1.5em;
  text-align:center;
}

.payback-value {
  font-size: 3em;
}
</style>
