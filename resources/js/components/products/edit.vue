<template>
    <div class="container">
        <h2 class="text-center">Atualizar Produto</h2>
        <div class="row">
            <div class="col-md-12">
                <router-link :to="{ name: 'ProductIndex' }" class="btn btn-primary btn-sm float-right mb-2">Back</router-link>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <form>
                    <div class="form-group">
                        <label>Nome</label>
                        <input type="text" class="form-control" v-model="product.name">
                    </div>
                    <div class="form-group">
                        <label>Preço</label>
                        <input type="text" class="form-control" v-model="product.price">
                    </div>
                    <div class="form-group">
                        <label>Peso</label>
                        <input type="number" class="form-control" v-model="product.weight">
                    </div>
                    <button type="button" class="btn btn-primary" @click="updateProduct()"> Editar </button>
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
        mounted() {
            this.editProduct(this.$route.params.productId);
        },
        methods: {
            editProduct(productId) {
                this.axios.get(`http://127.0.0.1:8000/api/products/${productId}`)
                   .then((response) => {
                       this.product = response.data;
                   });
            },
            updateProduct() {
                this.axios
                    .patch(`http://127.0.0.1:8000/api/products/${this.$route.params.productId}`, this.product)
                    .then((response) => {
                        this.$router.push({ name: 'ProductIndex' });
                    });
            }
        }
    }
</script>