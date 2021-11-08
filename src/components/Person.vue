<template>
    <div class="outer">
        <img :class= "personInfo.gender" :src="personInfo.picture" :alt="personInfo.firstName" />
        <h1>{{personInfo.firstName}} {{personInfo.lastName}}</h1>
        <h3>{{personInfo.email}}</h3>
        <button :class= "personInfo.gender" @click="getUser">Get Random User</button>
    </div>
</template>

<script>

export default {
  name: 'Person',
  data() {
      return {
        personInfo : {
            firstName : 'John',
            lastName : 'Doe',
            email : 'john@gmail.com',
            gender : 'male',
            picture : 'https://randomuser.me/api/portraits/men/10.jpg'
        }
      }
  },
  methods : {
      async getUser() {
          const res = await fetch('https://randomuser.me/api')
          const {results} = await res.json()
          //console.log(results)

          this.personInfo.firstName = results[0].name.first,
          this.personInfo.lastName = results[0].name.last,
          this.personInfo.email = results[0].email,
          this.personInfo.gender = results[0].gender,
          this.personInfo.picture = results[0].picture.large
      }
  }
}

</script>

<style scoped>
html,
body {
    font-family: Arial, Helvetica, sans-serif;
}

img {
    border-radius: 50%;
    border: 5px solid;
}

h1,
h3 {
    font-weight: normal;
}

.male {
    border-color: darkgreen;
    background-color: darkgreen;
}

.female {
    border-color: indigo;
    background-color: indigo;
}

button {
    cursor: pointer;
    color: white;
    border: 0;
    padding: 1rem 1.5rem;
}
</style>