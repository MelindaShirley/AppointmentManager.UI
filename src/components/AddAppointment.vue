<template>
    <div>
       <form 
  @submit="checkForm"
    novalidate="true"
>

<p v-if="errors.length">
    <b>Please correct the following error(s):</b>
    <ul>
      <li v-for="error in errors" v-bind:key="error" class="li">{{ error }}</li>
    </ul>
  </p>
                    <table class="border">
                    <tr style="width:100%">
                      <td>
                             <span class="input-group-text">Title</span>
                        </td>
                        <td  >
                            <input type="text" class="inputBorder"  v-model="title"  >
                       </td>
                    </tr>
                      <tr style="width:100%">
                        <td>
                             <span class="input-group-text">Customer Name</span>
                        </td>
                        <td  >
                            <input type="text" class="inputBorder"  v-model="customerName"  >
                       </td>
                    </tr>
                     <tr style="width:100%">
                        <td>
                             <span class="input-group-text">Email</span>
                        </td>
                        <td  >
                            <input type="email" class="inputBorder"  v-model="email"  >
                       </td>
                    </tr>
                     <tr style="width:100%">
                        <td>
                             <span class="input-group-text">Phone Number</span>
                        </td>
                        <td  >
                            <input type="number" class="inputBorder"  v-model="phoneNumber" maxlength="10" minlength="10">
                       </td>
                    </tr>
                    <tr>
                        <td>
                              <span class="input-group-text">Start Time</span>
                       </td>
                                  
                            <datetime v-model="startTime" type="datetime" zone="local"></datetime>
                        
                    </tr>
                    <tr>
                          <td>
                               <span class="input-group-text">End Time</span>
                        </td>
                        <td>
                               <datetime v-model="endTime" type="datetime" zone="local"></datetime>
                        </td>
                    </tr>
                    
                </table>
            <div>   </div>
                <span class="btn">  <input
      type="submit"
      value="Add New Appointment"
    >
                </span>
        </form> 
           </div>
</template>
<script>

import Moment from 'moment';
import axios from 'axios';

export default {
      name:"AddAppointment",
   props:["appointment"],
   components: {
    
  },

   data(){
return{
    appointments:[],
    customerName: "",
    title:"",
    startTime:"",
    endTime:"",
    errors: [],    
    startTimeFormatted:""   ,
    endTimeFormatted:""   ,
    email:"",
    phoneNumber:""
    
}
   },
 
   methods:{
             checkForm: function (e) {
      this.errors = [];
     
   
 let currentDate = new Date().toISOString();
console.log(currentDate);
//let testMel=new Date(this.startTime);
//testMel.toLocaleTimeString();
//console.log(testMel)
//let test=this.startTime
//test=Moment.utc(this.startTime).format('MM DD YYYY, HH:mm:ss a');
//console.log(test)
//this.startTimeFormatted=Moment(test).toISOString();
//console.log(this.startTimeFormatted);
//let test1=Moment.utc(this.endTime).format('MM DD YYYY, HH:mm:ss a');
//this.endTimeFormatted=Moment(test1).toISOString();
//console.log(this.endTimeFormatted);
            //this.startTimeFormatted.format();
             //this.endTimeFormatted = Moment(this.endTime, "YYYY-MM-DD HH:MM");
             this.startTimeFormatted=Moment(this.startTime).toISOString();
             this.endTimeFormatted=Moment(this.endTime).toISOString();
              if (!this.title) {
        this.errors.push("Title is required.");
      }
            if (!this.customerName) {
        this.errors.push("Customer Name is required.");
      }
       if (!this.email) {
        this.errors.push("Email is required.");
      }
      else if (!this.validEmail(this.email)) {
        this.errors.push('Valid email required.');
      }
      if (!this.phoneNumber) {
        this.errors.push("Phone Number is required.");
      }
  
      if (!this.email) {
        this.errors.push("Customer Name is required.");
      }
      if (!this.phoneNumber) {
        this.errors.push("Customer Name is required.");
      }
      if (!this.startTime) {
        this.errors.push('Start Time is required.');
      } else if (this.startTime< currentDate) {
       this.errors.push('You cannot book back dated appointments');
      }

       if (!this.endTime) {
        this.errors.push('End Time is required.');
      } else if (this.endTime< currentDate || this.endTimeFormatted<this.startTimeFormatted) {
       this.errors.push('End time cannot be less than start time');
      }

      if (!this.errors.length) {
        this.addAppointment();
      }else{
         this.$fire({
  title: "Uh-Oh!!",
  text: "Kindly fix the mentioned errors",
  type: "error",
  timer: 3000
}).then(r => {
 console.log(r.value);
});
      }

      e.preventDefault();
    }, validEmail: function (email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
       },
       addAppointment(){
                        
         axios.post("https://localhost:44332/api/"+"AppointmentDetails/",{
                CustomerName:this.customerName,
                StartTime:this.startTimeFormatted,
                EndTime:this.endTimeFormatted,
                Title:this.title,
                Email:this.email,
                PhoneNumber:this.phoneNumber
            })
            .then((response)=>{
              if(response.data=="Successful")
              {
               this.$fire({
  title: "Hurray!!",
  text: response.data,
  type: "success",
  timer: 3000
})
.then(r => {
 console.log(r.value);
})
.catch(error=>{console.log(error),this.$alert('Some Error occured')})   
this.$router.push({
        name: "Home", //use name for router push
       
     });  
              }
              else
              {
   this.errors.push(response.data)                 
                   this.$fire({
  title: "Uh-Oh!!",
  text: "Kindly fix the mentioned errors",
  type: "error",
  }).then(r => {
 console.log(r.value);
});
              }         
         })
            ;
               
        },
       
   },
   
   
}
</script>

<style scoped>
.border{
    min-width: 226px;
    width: 100%;
    height: 30px;
    padding: 3px;
    border: 1px solid #ddd;
}
.inputBorder{
    text-align: left; 
    border: 1px solid #ddd;
}
.btn
{
    align-content: center;
}
.li
{
  color: red;
}

tr:nth-child(even) {background-color: #f2f2f2;}
</style>

