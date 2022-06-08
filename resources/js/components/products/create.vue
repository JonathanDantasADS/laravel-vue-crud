<template>
    <div class="container">
        <h2 class="text-center">Criar Produto</h2>
        <div class="row">
            <div class="col-md-12">
                <router-link :to="{ name: 'ProductIndex' }" class="btn btn-primary btn-sm float-right mb-2">Voltar</router-link>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <form>
                    <div class="form-group">
                        <label>Nome</label>
                        <input type="text" class="form-control" v-model="product.name" placeholder="Informe o nome do produto">
                    </div>
                    <div class="form-group">
                        <label>Preço</label>
                        <input type="number" class="form-control" v-model="product.price" placeholder="0,00">
                    </div>
                    <div class="form-group">
                        <label>Peso</label>
                        <input type="number" class="form-control" v-model="product.weight" placeholder="Ex: 1.000">
                    </div>
                    <button type="button" class="btn btn-primary" @click="createProduct()">Criar</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                product: {}
            }
        },
        methods: {
            createProduct() {
                this.axios.post('http://127.0.0.1:8000/api/products', this.product)
                    .then(response => {
                        this.$router.push({ name: 'ProductIndex' })
                    })
                    .catch(error=>{
                      console.log(error)
                    })
            }
        }
    }
</script>