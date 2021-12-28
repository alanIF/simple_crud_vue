<template>
        <div class="card bg-primary text-white">
         <div class="card-header">
           <b>Atualizar Cidade</b>
        </div>
          <div class="card-body">

                <div class="form-group">
                    <input type="text" class="form-control" name="nome" v-model="nome" placeholder="Nome" >
                </div>
                  <div class="form-group">
                    <input type="number" class="form-control" name="latitude" v-model="latitude"  placeholder="latitude" >
                </div>
                <div class="form-group">
                    <input type="number" class="form-control" name="longitude" v-model="longitude"   placeholder="Longitude" >
                </div>

                <button type="submit"   @click="updateCidade()"  class="btn btn-primary">Atualizar</button>
          </div>
    </div>
</template>
<script>
export default {
  name: "editCidade",
  props: ["id"], 
   data() {
    return {
      cidade:null,
      nome: null,
      latitude: null,
      longitude: null
     }
  },
  methods: {
     async getCidade(id) {
        const req = await fetch(`http://127.0.0.1:8000/api/cidade/${id}`);
        const data = await req.json();
        this.cidade = data;
        console.log(this.cidade);
        this.nome= this.cidade.cidade;
        this.latitude= this.cidade.cords.latitude;
        this.longitude= this.cidade.cords.longitude;
    },
    
    async updateCidade() {
        const data = {
            id: this.cidade.id,
            nome: this.nome,
            latitude: this.latitude,

            longitude:this.longitude
        }
        const dataJson = JSON.stringify(data)    
        const req = await fetch(`http://127.0.0.1:8000/api/cidade/update/${this.cidade.id}`, {
          method: "PUT",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });
        const res = await req.json()
        console.log(res)
        location.reload()

      }
    },
  
  mounted(){
      this.getCidade(this.id);
  }

}
</script>
