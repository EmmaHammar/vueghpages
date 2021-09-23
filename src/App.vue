<template>
  <div id="app">
    <h1>Hello VUE</h1>
    <!-- <p>Välkommen {{userName}}</p> -->
    <p>Välkommen {{ user.firstName }} {{ user.lastName }}</p>

    <!-- räknar-exemplet: -->
    <div>
      Du har klickat {{ clicked }} ggr
      <button @click="onClick">Klicka</button>
    

      <!-- vill visa nedan div när vi klickat 5 ggr. v- ser Vues inbyggda alternativ. Vue använder inte hide utan Bra-klickat existerar inte i DOMen förrän v-if har blivit true. -->
      <div v-if="clicked > 5">
        Bra klickat!
      </div>

    
      <!-- förifyllda värden: v-model="user.firstName" -->
      <form @submit="handleSubmit">
        Förnamn: <input type="text" v-model="user.firstName" id="firstName"> <br />
        Efternamn: <input type="text" v-model="user.lastName" id="lastName"> <br />
        <button>Spara</button>
      </form>
      
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',

  //detta kan vara strängar, tal, listor, booleans - alla typer som JS kan hantera
  data() {
    return {
      // userName: "Janne",
      // user: {firstName: "Janne", lastName: "Kemi"},
      user: {firstName: localStorage.getItem("firstName"), lastName: localStorage.getItem("lastName")},
      clicked: 0,
    }
  }, 

  methods: {
    onClick() {
      console.log("klick på knapp");
      this.clicked ++
    },
    handleSubmit(event) {
      event.preventDefault();

      //fånga värdet
      console.log("formulär sparat", event.target.firstName.value);

      //spara i lS. //stringify för att spara, parse för att hämta. men i ex gör 2 olika:
      localStorage.setItem("firstName", event.target.firstName.value)
      localStorage.setItem("lastName", event.target.lastName.value)

    }

  }

}

//skapa en data
//allt som vi skriver i script måste vi exportera som defaults. Om vi har data som vi har tillgång till o vill visa i komponenten måste det finnas innanför export default
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
