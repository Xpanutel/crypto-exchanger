<script>
import CryptoConvert from 'crypto-convert';
import Input from './components/input.vue'
import Selector from './components/selector.vue'

const convert = new CryptoConvert();

export default {
  components: { Input, Selector },
  data () {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0
    }
  },
  methods: {
    changeAmount(val) {
      this.amount = val
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      if(this.amount <= 0) {
        this.error = 'Введите значение больше 0';
        this.result = 0;
        return;
      } else if(this.cryptoFirst == this.cryptoSecond) {
        this.error = 'Выберите разные валюты для конвертации';
        this.result = 0;
        return;
      } else if(this.cryptoFirst == '' || this.cryptoSecond == '') {
        this.error = 'Выберите валюты для конвертации';
        this.result = 0;
        return;
      }
      
      this.error = ''

      await convert.ready();
      if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH')
        this.result = convert.BTC.ETH(this.amount);
      else if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT')
        this.result = convert.BTC.USDT(this.amount);
      else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC')
        this.result = convert.ETH.BTC(this.amount);
      else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT')
        this.result = convert.ETH.USDT(this.amount);
      else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC')
        this.result = convert.USDT.BTC(this.amount);
      else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH')
        this.result = convert.USDT.ETH(this.amount);
    }
  }
}  
</script>

<template>
  <h1>CRYPTO</h1>
  <Input :changeAmount="changeAmount" :convert="convert"/>
  <p v-if="error != ''" className='error'>{{ error }}</p>
  <p v-if="result != 0" className='result'>{{ result }}</p>
  <div className='selectors'>
    <Selector :setCrypto="setCryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond"/>
  </div>  
</template>

<style scoped>
.selectors {
  display: flex;
  justify-content: center;
  gap: 100px;
  margin-top: 0 auto;
}
</style>