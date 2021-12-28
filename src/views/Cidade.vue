<template>
    <div>
     <table id="tabela" class="table table-hover tabela" style="width: 100%" >
    <thead>
      <tr>
        <th>Nome</th>
        <th>Latidude</th>
        <th>Longitude</th>
        <th>Ações</th>
     
        </tr>
    </thead>
    <tbody>
     <tr v-for="cidade in cidades" :key="cidade.id">
         <td>{{cidade.nome}}</td>
        <td>{{cidade.latitude}}</td>

        <td>{{cidade.longitude}}</td>
        <td >  <button class="btn btn-info" @click="edit(cidade.id)"><i class="fa fa-pencil"></i></button> <button class="btn btn-danger" @click="deleteCidade(cidade.id)"><i class="fa fa-trash"></i></button></td>

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
   <div v-if="addVisible">
       <addCidade />
   </div>
   
   <div v-if="editVisible">
       <editCidade :id="idCidade" />

   </div>
      
</template>

<script>
  import addCidade from '../components/cidade/addCidade.vue'
  import editCidade from '../components/cidade/editCidade.vue'

  export default {

 name: "Cidade",
    data() {
      return {
        cidades: null,
        addVisible:false,
        editVisible:false,
        idCidade:null
      }
    },
    components:{
        addCidade,
        editCidade
    },
    methods: {
      async getCidades() {
        const req = await fetch('http://127.0.0.1:8000/api/cidade/');
        const data = await req.json();
        this.cidades = data.data;
      },
      
      async deleteCidade(id) {
        const req = await fetch(`http://127.0.0.1:8000/api/cidade/delete/${id}`, {
          method: "DELETE"
        });
        const res = await req.json()
        location.reload();

      },
      add(){
          this.addVisible=true;
          this.editVisible=false;
      },
      edit(id){
          this.addVisible=false;
          this.editVisible=true;
          this.idCidade=id;
      }
    
    },
     mounted () {
        this.getCidades()
    }
  }
</script>
 