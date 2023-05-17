<template>
  <div>
    <div style="background-color: red;">
    <h1 id="Heading">URL Shortner</h1>
    <div class="input_div">
    <input id="input_" ref="inputURl" placeholder ='https://example/long_url.com' type="Text">
    <button id="btn" @click="GenerateURl">Generate</button>
    </div>
  </div>
  <div class="URL_shower">
      <h1>Your Shortened URL would be shown below</h1>
    </div>
  </div>
  <div>
    <div class="card-container">
      <div
      v-for="URL in ArrUrl"
     :key="URL.id"
      class="crd"
      >
      <p  ref="URL">
        {{ URL.text }}
      </p>
      <button id="btn2" @click="copyclipboard">📋</button>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data(){
    return{
      ArrUrl:[],
      GenURl:[]
    }
  },
  methods:{
    GenerateURl()
    {
      let input = this.$refs.inputURl.value;
      if(input ==='' || !input.includes('http'))
      {
        alert('Enter a Valid URL');
        return;
      }
      axios.get(`https://tinyurl.com/api-create.php?url=${encodeURIComponent(input)}`).then(response=>{
        console.log('woked', response);
        this.ArrUrl.push({
        id: Math.floor(Math.random() * 10000),
        text:response.data,
      })
      })
      this.$refs.inputURl.value = ''
      console.log(this.$refs.inputURl.value);
    },
    copyclipboard()
    {
      alert('Work in Progress');
    }
  }
}
</script>

<style>
#btn2{
  display: flex;
  font-size: 20px;
  border: none;
  background: none;
  
}
.card-container
{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.crd
{
  margin-top: 20px;
  background: linear-gradient(90deg, hsla(20, 89%, 89%, 1) 0%, hsla(324, 57%, 77%, 1) 50%, hsla(278, 54%, 81%, 1) 100%);;
  height: 80px;
  width:50%;
  padding-left: 20px;
    padding-top: 20px;
}
#Heading{
  display: flex;
  justify-content: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  font-weight: bold;
  font-size: 4rem;
  color: 100%;
}
.input_div{
  display: flex;
 justify-content: center;
}
#input_{
  display: flex;
  color: red;
  width: 800px;
  font-weight: bold;
  border-style:outset;
  border-color:red;
  padding-left:20px ;
  height: 50px;

}
#btn{
  height: 50px;
  margin-left: 20px;
  width:auto;
  padding-right: 20px;
  padding-left: 20px;
  font-weight: bolder;
  border-radius: 7px;
  font-size: 15px;
  color: white;
  background:rgb(214, 136, 18);

}
.URL_shower{
  display: flex;
  margin-top: 20px;
  justify-content: center;
}
</style>
