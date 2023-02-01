<template>
  <!-- <h2>Sign Up Form</h2> -->
  <form @submit.prevent="submit">
    <label>Email</label>
    <input type="email" v-model="email" required>
    <label>Password</label>
    <input type="password" v-model="password" required>
    <p v-if="errMsg" class="error">{{errMsg}}</p>
    
    <label>Roles</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>
    
    <label>Skills</label>
    <input type="text" @keyup.alt="addSkill" v-model="skill">
    <div v-for="skill in skills" :key="skill">
        <p>{{skill}} <span class="cross" @click="deleteSkill(skill)">&#10006</span></p>
    </div>
    <div>
        <input type="checkbox" v-model="accept">
        <label>Accept Terms & Conditions</label>
    </div>
    <div class="buttonAlign">
        <button class="create">Create Account</button>
    </div>
 
  </form>
  <!-- <p>Email - {{email}}</p>
  <p>Password - {{password}}</p>
  <p>Role - {{role}}</p>
  <p>single- {{accept}}</p> -->
</template>

<script>
export default {
    data(){
        return{
            email:"",
            password:"",
            role:"designer",
            accept: false,
            skills:[],
            skill:"",
            errMsg:"",
        }
    },
    methods:{
        addSkill(e){
            if(e.key==="," && this.skill){
                this.skills.push(this.skill);
                this.skill="";
            }   
        },
        deleteSkill(skill){
            this.skills= this.skills.filter(loopSkill=>{
                return loopSkill!= skill;
            })
        },
        submit(){
            if(this.password.length < 8){
                this.errMsg="Password Must be 8 Char"
            }
        }
    }
}
</script>

<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background-color: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input,select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 3px;
    }
    .cross{
        cursor: pointer;
        color: crimson;
    }
    .create{
        background-color: royalblue;
        padding:8px;
        color: white;
        border-radius: 10px;
    }
    .buttonAlign{
        text-align: center;
    }
    .error{
        color: crimson;
    }

</style>