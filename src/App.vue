<script>
export default {
  data() {
    return {
      number: '',
      rule: 15,
      message:'Digite o número acima...',
      call:false,
    }
  },

  methods: {
    handleMessageButton(){
      if(this.number.length === this.rule){
        this.message = 'Chamar'
        this.call = true
        return
      }

      this.message = 'Digite o número acima...'
      this.call = false
    }, 
    handleFormatCall(value){
      const numberCall = value
      .replace(/(\d{2})(\d)/, '($1) $2')
			.replace(/(\d{4})(\d)/, '$1-$2')
			.replace(/(\d{4})-(\d)(\d{4})/, '$1$2-$3')
			.replace(/(-\d{4})\d+$/, '$1')
      this.number = numberCall

      this.handleMessageButton()
    },
    handleReplaceToNumber(value){
      return value.replace(/\D/g,'')
    },
    onChange(e){
      const onlyNumber = this.handleReplaceToNumber(e.target.value)
      this.handleFormatCall(onlyNumber)
    }
  }
}
</script>

<template>
  <main>
    <img alt="Flame in zap logo" class="flameLogo" src="./assets/logo.png" />

    <input type="text" @input="onChange" maxlength="15" v-model=this.number placeholder="Digite o número aqui">
    <a :href="`https://wa.me/${this.handleReplaceToNumber(number)}`" class="buttonCall" :class="{'active' : this.call }">
      {{ this.message }}
    </a>

  </main>

  <footer>
    <a className="version" target="_blank" :href="`https://web.whatsapp.com/send/${this.handleReplaceToNumber(number)}`">V.5.0</a>
    <div class="social">
      <a href="https://www.linkedin.com/in/geanlopes/" target="_blank" class="">LinkedIn</a>
      <a href="mailto:f.geanlopes@gmail.com" target="_blank" class="">Email</a>
      <a href="https://github.com/fgeanlopes" target="_blank" class="">GitHub</a>
    </div>
  
  </footer>

</template>