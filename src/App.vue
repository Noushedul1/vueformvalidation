<template>
  <div id="app">
    <form @submit.prevent="submithandle">
      <div>
        <label>First name : </label>
        <input type="text" v-model.lazy="formData.firstname">
      </div>
      <div>
        <label>Last name : </label>
        <input type="text" v-model.lazy="formData.lastname">
      </div>
      <div>
        <label>Password: </label>
        <input type="text" v-model.lazy="formData.password">
        <p v-if="formData.errpass">{{formData.errpass}}</p>
      </div>
      <div>
        <label>Position :</label>
        <select v-model="formData.position">
          <option>Web Design</option>
          <option>Graphic Design</option>
          <option>UI/UX Designer</option>
          <option>Web Development</option>
          <option>Excel</option>
        </select>
      </div>
      <div>
        <label>Skill :</label>
        <input type="text" v-model="formData.
        tempSkill" @keyup.alt="press">
        <div v-for="skill in formData.skills" :key="skill" class="pill">
          <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>
      </div>
      <div>
        <input type="radio" v-model="formData.terms">
        <label>I agree with this rule.</label>
      </div>
      <input type="submit" value="Submit">
    </form>
    <div>
    <p>First name : {{formData.firstname}}</p>
    <p>Last name : {{formData.lastname}}</p>
    <p>Password name : {{formData.password}}</p>
    <p>Terms : {{formData.terms}}</p>
    <p>Position : {{formData.position}}</p>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'App',
    data() {
      return {
        formData: {
          firstname: '',
          lastname: '',
          password: '',
          terms: false,
          position: '',
          tempSkill: '',
          skills: [],
          errpass: ''
        }
      }
    },
    methods: {
      press(e) {
        if(e.key === ',' && this.formData.tempSkill){
          if(!this.formData.skills.includes(this.formData.tempSkill)){
             this.formData.skills.push(this.formData.tempSkill);
          }
          this.formData.tempSkill = '';
        }
      },
      deleteSkill(skill){
        this.formData.skills = this.formData.skills.filter((item)=>{
          return skill !== item;
        })
      },
      submithandle() {
        this.formData.errpass = (this.formData.password.length > 6) ? '' : 'password is more than 6 char. ';
      }
    }
  }
</script>
<style scoped>
.pill{
  background: #ddd;
  padding: 10px;
  width: 100px;
  margin: 10px;
  border-radius: 10px;
  text-align: center;
}
</style>
