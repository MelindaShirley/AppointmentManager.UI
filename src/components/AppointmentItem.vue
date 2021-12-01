<template>
    <div>
       <table class="table">
            <tr>
                <td class="td" >{{appointment.title}}</td>
                <td class="td">{{appointment.customerName}}</td>
                <td class="td">{{appointment.email}}</td>
                <td class="td">{{appointment.phoneNumber}}</td>
                <td class="tdDate" >{{appointment.startTime | formatDate}}</td>
                <td class="tdDate">{{appointment.endTime | formatDate}}</td>
                <td class="icon"> 
                <button type="button"
                class="btn btn-light mr-1"
                        v-on:click="updateAppointment">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                    <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                    <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                    </svg>
                </button>
                   
                   <button type="button"
                class="btn btn-light mr-1" id=""
                        v-on:click="deleteAppointment">
                       <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash-fill" viewBox="0 0 16 16">
                        <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
                        </svg>
                </button>
                    
              </td>
            </tr>
        </table>
          </div>
</template>

<script>


import axios from 'axios';
export default {
    name:"AppointmentItem",
    props:["appointment"],
    methods: {
        updateAppointment(){
            console.log(this.appointment.startTime);
      let appointmentToUpdate = {
        appointmentId: this.appointment.appointmentId,
        customerName: this.appointment.customerName,
        startTime:this.appointment.startTime,
        endTime:this.appointment.endTime,
        title: this.appointment.title,
        email:this.appointment.email,
        phoneNumber:this.appointment.phoneNumber
      };
        this.$router.push({
        name: "editAppointment", //use name for router push
        params: { appointmentToUpdate }
      });
    },
     deleteAppointment(){
        axios.delete("https://localhost:44332/api/"+"AppointmentDetails/"+this.appointment.appointmentId)
.then(
location.reload())
.catch(error=>{console.log(error),this.$alert('Some Error occured')});
          
      
    }
  }
 
    }
</script>

<style scoped>
    .td{
      width: 150px;
 padding-right: 75px;
  border-right: 50px;
            word-wrap: break-word;
    }
    .icon{
      width: 75px;
              
    }
     .tdDate{
      width: 150px;
 padding-right: 75px;;
  border-right: 50px;
  white-space: nowrap;
    }
    .table
    {
         border-collapse: collapse;
        table-layout: fixed;
        width: 310px;
         border: solid 1px #666;
    }
    tr:nth-child(even) {background-color: #f2f2f2;}
</style>