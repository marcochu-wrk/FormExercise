<template>
    <form @submit.prevent="handleSubmit">
        <h1>Submission Form</h1>
        <label>Email:</label>
        <input type="email" required v-model="email">

        <label>Password:</label>
        <input type="password" required v-model="password">
        <div v-if="passwordErr" class="error">{{ passwordErr }}</div>

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">

        <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill(skill)">
            {{ skill }}
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept Terms and Conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>
    </form>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>User: {{ role }}</p>
    <p>Terms Accepted: {{ terms }}</p>
</template>

<script>
export default{
data(){
    return{
        email: '',
        password:'',
        role: 'designer',
        terms: false,
        tempSkill: '',
        skills:[],
        passwordErr:''
    }
},
methods:{
    addSkill(e){
        if(e.key === 'Enter' && this.tempSkill){
            if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill)
            }       
            this.tempSkill = ''
        }
    },
    deleteSkill(deleteSkill){
        if(this.skills.includes(deleteSkill)){
        //    var arrPos = this.skills.indexOf(deleteSkill)
        //     this.skills.splice(arrPos, 1)
            this.skills = this.skills.filter((item) => // Creates a new array of skills in item, then checks each item and compares whether deleteSkill = item, if it does it removes it from the item array. Once done it passes it back to the original array
             deleteSkill !== item)
        }
    },
    handleSubmit(){

        this.passwordErr = this.password.length > 5 ? '' : 'Password must be 6 characters long'
        console.log('form submitted')
    }
}
}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
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
    top: 2px;
}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 2px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button{
    background: rgb(65, 65, 195);
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
</style>