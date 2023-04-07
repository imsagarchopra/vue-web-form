<template>
   <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email"/>

    <label>Password:</label>
    <input type="password" required v-model="password"/>
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill"/>
    <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required/>
        <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Create an Account</button>
    </div>
   </form>
</template>

<script>
    export default {
        data(){
            return{
                email:'',
                password: '',
                role: '',
                terms: false,
                tempSkill: '',
                skills:[],
                passwordError: ''
            }
        },
        methods:{
            addSkill(e){
                if(e.key === ',' && this.tempSkill){
                    if(!this.skills.includes(this.tempSkill)){
                        this.skills.push(this.tempSkill);                       
                    }      
                    this.tempSkill = '';            
                }
            },
            deleteSkill(skill){
                this.skills = this.skills.filter((item) => {
                    return skill !== item
                })
            },
            handleSubmit(){
                //Validate Password
                //this.passwordError = thi.password.length > 5 ? '' : 'Password must be atleast 5 chars long'
            }
        }
    }
</script>

<style scoped>
form {
  background: linear-gradient(45deg, rgb(225, 225, 225), rgb(215, 215, 215));
  /* background: white; */
  width: 450px;
  text-align: left;
  margin: 0 auto;
  padding: 3rem;
  display: inline-block;
  border-radius: 16px;
}

label {
  font-size: large;
  text-transform: uppercase;
  color: #999;
  font-weight: bold;
  letter-spacing: 2px;
  display: inline-block;
  margin-bottom: 0.3rem;
}

input, select {
  background-color: rgb(235, 235, 235);
  /* background-color: white; */
  display: block;
  box-sizing: border-box;
  width: 100%;
  margin-bottom: 1.2rem;
  border: none;
  padding: 1.5rem 6px;
  font-size: large;
  color: #888;
  border-radius: 16px;
  box-shadow: 0 4px 3px 0px rgb(182, 182, 182);
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
    margin-bottom: 0.3rem;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }

.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }

button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>