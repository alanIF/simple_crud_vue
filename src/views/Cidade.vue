<template>
    <div>
     <table class="table table-hover" >
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
        <td> <button class="btn btn-info" @click="atualizarCidade(cidade.id)">Atualizar</button> <button class="btn btn-danger" @click="deleteCidade(cidade.id)">delete</button></td>

     </tr>
    </tbody>
  </table>

    </div>
   
   
</template>

<script>
  export default {

 name: "Cidade",
    data() {
      return {
        cidades: null
      }
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

      }
    },
     mounted () {
        this.getCidades()
    }
  }
</script>
 