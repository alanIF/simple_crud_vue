<template>
    <div>
        <form method="POST" @submit="createCidade" >
                <div class="form-group">
                    <input type="text" class="form-control" name="nome" v-model="nome" placeholder="Nome" >
                </div>
                  <div class="form-group">
                    <input type="number" class="form-control" name="latitude" v-model="latitude"  placeholder="latitude" >
                </div>
                <div class="form-group">
                    <input type="number" class="form-control" name="longitude" v-model="longitude"   placeholder="Longitude" >
                </div>

                <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
</template>

<script>
export default {
  name: "addCidade",
  data() {
    return {
      nome: null,
      latitude: null,
      longitude: null,
     }
  },
  methods: {
    
    async createCidade(e) {
      e.preventDefault()
      const data = {
        nome: this.nome,
        latitude: this.latitude,

        longitude:this.longitude
        
      }
      const dataJson = JSON.stringify(data)    
      const req = await fetch("http://127.0.0.1:8000/api/cidade/store", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });
      const res = await req.json()
      console.log(res)
      msg = "Cidade criada com sucesso!"
      // clear message
      setTimeout(() => this.msg = "", 3000)
      // limpar campos
      this.nome = ""
      this.latitude = ""
      this.longitude = ""
    location.reload();

      
    }
  }
  
}
</script>
