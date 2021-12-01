<template>
<div>
    <table class="table">
        <tr>
              <td class="td" >Title</td>
                <td class="td">Customer Name</td>
                <td class="td">Email</td>
                <td class="td">Phone Number</td>
                <td class="tdDate" >Start Time</td>
                <td class="tdDate">End Time</td>
                <td class="icon">Options</td>
        </tr>
    </table>
   <div v-bind:key="appointment.appointmentId" v-for="appointment in appointments">
        <table >
                       <tr>
                     <AppointmentItem v-bind:appointment= "appointment" v-on:del-appointment="$emit('del-appointment',appointment.appointmentId)" />
            </tr>
        </table>
           
   </div>

</div>  
</template>

<script>

import AppointmentItem from './AppointmentItem.vue'
export default {
    name:"Appointments",
    components:{
        AppointmentItem
    },
    props:["appointments"]
}

</script>

<style scoped>
  .table
    {
         border-collapse: collapse;
        table-layout: fixed;
        width: 310px;
         border: solid 1px #666;
         background-color: black;
         color: white;
    }
    tr:nth-child(even) {background-color: #f2f2f2;}
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
</style>