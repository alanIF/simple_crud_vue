<template>
    <div>
     <table id="tabela" class="table table-hover tabela" style="width: 100%" >
    <thead>
      <tr>
        <th>Reservatorio</th>
        <th>Latidude</th>
        <th>Longitude</th>
        <th>Ações</th>
     
        </tr>
    </thead>
    <tbody>
     <tr v-for="posto in postos" :key="posto.id">
         <td>{{posto.reservatorio}}</td>
        <td>{{posto.latitude}}</td>

        <td>{{posto.longitude}}</td>
        <td >  <button class="btn btn-info" @click="edit(posto.id)"><i class="fa fa-pencil"></i></button> <button class="btn btn-danger" @click="deletePosto(posto.id)"><i class="fa fa-trash"></i></button></td>

     </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="1"><button class="btn btn-primary" @click="add()"><i class="fa fa-plus"></i></button></td>
            <td colspan="4"></td>

        </tr>
    </tfoot>
  </table>

    </div>
   
      
</template>

<script>


  export default {

 name: "Posto",
    data() {
      return {
        postos: null,
        
        idPosto:null
      }
    },
    components:{
        
    },
    methods: {
      async getPostos() {
        const req = await fetch('http://127.0.0.1:8000/api/posto/');
        const data = await req.json();
        this.postos = data.data;
      },
      
      async deletePosto(id) {
        const req = await fetch(`http://127.0.0.1:8000/api/posto/delete/${id}`, {
          method: "DELETE"
        });
        const res = await req.json()
        location.reload();

      },
     
    
    },
     mounted () {
        this.getPostos()
    }
  }
</script>
 