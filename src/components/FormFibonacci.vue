<template>
  <div>
	<b-form>
		<b-form-group
			label="Número:"
			label-for="numero"
			description="Ingresa un número"
		>
			<b-form-input
				v-model="numero"
				type="text"
				required
				placeholder="Ingresa un número"
			></b-form-input>
		</b-form-group>

		<b-button type="button" variant="primary" @click="onSubmit" >Buscar</b-button>
	  
	</b-form>
	<h4>Número inmediato Fibonacci: <b-badge  class="lead" v-html="resultado"></b-badge></h4>
  </div>
</template>

<script>
import { ValidationProvider, extend } from 'vee-validate';
import { required } from 'vee-validate/dist/rules';

extend('required', {
  ...required,
  numero: 'Es requerido'
});

export default {
    name: 'FormFibonacci',
    data() {
        return {
            numero: '',
            resultado: ''
        }
    },
    methods: {
        onSubmit () {

        	if(this.numero.length < 1){
        		this.$swal.fire({
					position: 'top-end',
					icon: 'error',
					title: 'El campo es obligatorio',
					showConfirmButton: false,
					timer: 1500
				})
				return false;
        	}


			this.$swal.fire({
				title: '¿Confirmar operación?',
				text: "",
				icon: 'warning',
				showCancelButton: true,
				confirmButtonColor: '#3085d6',
				cancelButtonColor: '#d33',
				confirmButtonText: 'Si, continuar',
				cancelButtonText: 'Cancelar',
			}).then((result) => {
				if (result.value) {
		        	let n = this.numero;
		        	this.resultado = this.inmediato(n);
		        	this.$swal.fire({
						position: 'top-end',
						icon: 'success',
						title: 'La petición se completo correctamente',
						showConfirmButton: false,
						timer: 1500
					})
				}
			})         
        	
        	//this.$swal('Hello Vue world!!!');

        },
        fib (n) {
		  if (n < 2){
		    return n
		  }
		  return this.fib(n - 1) + this.fib (n - 2)
		},
		inmediato (n) {
        	let i = 0;
        	let temp;
        	let res;
			while (i <= n){
				temp = this.fib(i);
				if(temp <= n){
					res = temp;
				}
				i++;
			}
			return res;
		},
		/*fun (n) {
			let temp = this.fib(n);
			console.log(n, temp);
			if(temp <= n){
				return temp;
			}
			
			return this.fun(n-1);
		}*/

    }
}
</script>
</script>