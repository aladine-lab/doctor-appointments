<template>
    <div class="head">
      <h2 @click="goback">DO <br> CS</h2>
      <font-awesome-icon icon="fa-regular fa-user" class="user"/>
    </div>
    <div class="content">

      <div class="info" v-if="doctor && rend">
        <img src="../assets/doc.png" alt="">
        <h1>Dr.{{doctor.name}}</h1>
        <p>Specialty : {{ doctor.specialty }}</p>
        <p>{{ doctor.workstation }}</p>
        <p style="font-size : 12px;"><font-awesome-icon icon="fa-regular fa-building" /> {{doctor.place }}</p>
        <div class="rating">
          <div class="ra">
            <h3 style="color: #6B7280; font-size: 17px;">Rating</h3>
            <p style="color: #6B7280; font-size: 49px;">4.3</p>
            <div class="stars">
            <font-awesome-icon icon="fa-solid fa-star" class="star"/>
            <font-awesome-icon icon="fa-solid fa-star" class="star"/>
            <font-awesome-icon icon="fa-solid fa-star" class="star"/>
            <font-awesome-icon icon="fa-solid fa-star" class="star"/>
            <font-awesome-icon icon="fa-regular fa-star" />
          </div>
            <p style="color: #6B7280; font-size: 11px; margin: 0">40000</p>
          </div>
          <div class="por">
            <div class="rat"><span>5</span> <div class="bar"> <span style="width: 80%;"></span></div></div>
            <div class="rat"><span>4</span> <div class="bar"> <span style="width: 20%;"></span></div></div>
            <div class="rat"><span>3</span> <div class="bar"> <span style="width: 30%;"></span></div></div>
            <div class="rat"><span>2</span> <div class="bar"> <span style="width: 15%;"></span></div></div>
            <div class="rat"><span>1</span> <div class="bar"> <span style="width: 5%;"></span></div></div>
          </div>
        </div>
      </div>

      <div v-else-if="doctor && !rend">rendez-vous</div>
      <div v-else>Loading info...</div>

      <button class="bt" @click="rendezVous">{{ rend ? 'Prender rendez-Voue' : 'Confirmer' }}</button>
    </div>
  </template>
  
  <script>
  export default {
    
    data() { 
      return {
        doctor : null,
        id : this.$route.params.id,
        rend : true
    }
  },
  mounted () {
    fetch("http://localhost:3000/doctors/" + this.id)
    .then(res => res.json())
    .then(data => this.doctor = data)
    .catch(err => console.log("hello"));
  },
  methods: {
    goback() {
      this.$router.go(-1);
    },
    rendezVous() {
      this.rend = !this.rend;
    }
  }
}
</script>
<style scoped>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 40px;
}

.info {
  position: relative;
  background-color: #F9FAFB;
  border-radius: 20px;
  width: 100%;
  text-align: center;
  /* padding: 30px; */
}
img {
  width: 138px;
    height: 138px;
    border-radius: 22px;
    position: absolute;
    top: -70px;
    left: 50%;
    transform: translateX(-50%);
}
h1 {
  color: #0E7490;
  font-size: 19px;
  margin-top: 80px;
}
.info p {
  color: #6B7280;
  font-size: 19px;
  margin: 0;
}

p:nth-child(4) {
  margin-top: 20px;
}

p:nth-child(5) {
  margin-top: 5px;
}
.stars {
  font-size: 10px;
}
.star {
  color: gold;
}
button {
  padding: 15px;
  border-radius: 10px;
  background-color: #0E7490;
  color: white;
  font-weight: bold;
  cursor: pointer;
  width: 100%;
  border: none;
  margin: 20px 0;
}

.rating {
  display: flex;
    justify-content: space-between;
    padding: 40px;
  align-items: center;
}

.por {
  flex-grow: 1;
}

.por .bar {
    width: 100%;
    height: 10px;
    background-color:#a8a8a8;
    border-radius: 20px;
}

.bar span {
  display: block;
    height: 100%;
    border-radius: 20px;
    background-color: rgb(14, 116, 144);
}
.por span {
  margin-right: 8px;
}
.por .rat {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 20px;
}
.head {
  padding: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}
.head h2 {
  color: #0E7490;
  font-size: 27px;
  font-weight: bold;
}
.user {
  width: 15px;
  height: 15px;
  cursor: pointer;
  padding: 15px;
  background-color: #F3F4F6;
  border-radius: 40%;
}
</style>