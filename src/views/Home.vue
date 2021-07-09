<template>
  <div class="home" :class="dark_theme? 'home_dark' : 'home_light'">

    <div class="header" :class="dark_theme? 'header_dark' : 'header_light'">
      <div class="item" > <img class="logo" src="../images/CS-Logo.png" alt="Logo">
      </div>
      <div class="item"> 
        <img v-if="!dark_theme" class="theme_button" src="../images/moon.png" alt="dark" v-on:click="dark_theme=!dark_theme"/>    
        <img v-if="dark_theme" class="theme_button" src="../images/sun.png" alt="light" v-on:click="dark_theme=!dark_theme"/>
      </div>
    </div>

    <hr v-if="dark_theme" style="margin:0px">

    <h1 class="title" :class="dark_theme? 'title_dark' : 'title_light'"> The 9 Leadership Types </h1>

    <div class="flex-container" v-if="leader_types">
      <div v-for="(leader_type, idx) in leader_types.types" :key="idx" class="leader" :style="{'background-color': leader_type.colour}">
          <h3 class="leader_title" :style="{'color': leader_type.colour}">{{leader_type.name[0].text}} </h3>
          <prismic-image :field="leader_type.exemplar_image" class="leader_image"/>
          <h4 class="sub-title">{{leader_type.description[0].text}}</h4>
          <p class="type-p">{{leader_type.description[1].text}}</p>
          <hr>
          <p class="atb">{{leader_type.description[2].text}}</p>
          <ul>
          <li class="bullets" v-for="(desc, idx) in leader_type.description.slice(3).filter(el=>el.text !== '')" :key="idx">{{desc.text}}</li>
        </ul>
      </div>
    </div>
    <br/>
    <div class="footer" :class="dark_theme? 'footer_dark' : 'footer_light'">
      <div> 
        <img class="logo-2" src="../images/Logo-2.png" alt="Logo-2">
      </div>
    </div>
  </div>
</template>

<script>
export default {  
  name: "Home",
  data: function () {
    return {
      leader_types: undefined,
      dark_theme: false
    }
  },
  async mounted(){
    const response = await this.$prismic.client.getByID('YG76KxMAACEAiboY')
    console.log(response)
    this.leader_types = response.data
  }
  
};
</script>
<style>
  * {
    box-sizing: border-box;
  }

  .home {
    font-family: Arial, Helvetica, sans-serif;
    margin: 0px;
    padding: 0px;
    width: 100%;
  }

  .header_light {
    background-color: #ccc;
  }

  .header_dark {
    background-color: black;
  }
  
  .home_light {
    background-color: #f4f4f4;
  }

  .home_dark {
    background-color: black;
  }

  .title_light {
     color: black;
  }

  .title_dark {
    color: #f4f4f4;
  }

 .footer_light {
    background-color: #f4f4f4;
  }

  .footer_dark {
    background-color: black;
  }

  .header {
    display: flex;
    flex-wrap: wrap;
    padding: 0px;
    height: 120px;
  }

 .item {
    margin: 10px;
    padding: 10px;
    text-align: center;
    border-radius: 10px;
    width: 400px;
  }

  .logo {
    width: 200px;
  }

  .theme_button {
    width: 50px;
    margin-top: 10px;
    cursor: pointer;
    position: absolute;
    top: 20px;
    right: 40px;
  }

  .title {
    text-align: center;    
  }

  .flex-container {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
  }

  .leader {
    background: #f4f4f4;
    border: dimgray solid 5px;
    margin: 10px;
    padding: 10px;
    text-align: center;
    border-radius: 10px;
    width: 400px;
    height: 730px;
    box-shadow: 10px 10px 10px dimgrey;
  }

  .leader:hover {
    background: rgba(62,62,62) !important;
    color: white;
    cursor: pointer;
    transform: scale(1.03);
    transition: all 1s ease;
  }

  .leader_title {
    background-color: black;
    width: 360px;
    text-align: center;
    padding: 5px;
    border: black solid 5px;
    text-transform: uppercase;
  }

  .sub-title {
    font-weight: bold;
    font-style: italic;
  }

  .type-p {
    text-align: left;
    font-weight: bold;
    font-style: italic;
    line-height: 18px;
  }

  .atb {
    font-weight: bold;
    font-size: 18px;
    text-align: left;
    margin-left: 10px;
  }

  .bullets {
    text-align: left;
    font-weight: bold;
    line-height: 25px;
  }

  .footer {
    display: flex;
    justify-content: center;
  }

  .logo-2 {
    width: 100px;    
  }

  .leader_card {
    border: 1px solid black;
    width: 500px;
    height: 500px;
  }

  .leader_image {
    width: 200px;
  }
</style>