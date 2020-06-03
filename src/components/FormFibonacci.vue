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

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class FormFibonacci extends Vue {
	private numero: string = '';
	private resultado: number | string = '';

	public onSubmit(): void {
		let n: any;

		if (this.numero.length < 1) {
			this.$swal.fire({
				position: 'top-end',
				icon: 'error',
				title: 'El campo es obligatorio',
				showConfirmButton: false,
				timer: 1500,
			});
		} else {
			this.$swal.fire({
				title: '¿Confirmar operación?',
				text: '',
				icon: 'warning',
				showCancelButton: true,
				confirmButtonColor: '#3085d6',
				cancelButtonColor: '#d33',
				confirmButtonText: 'Si, continuar',
				cancelButtonText: 'Cancelar',
			}).then((result: any) => {
				if (result.value) {
					n = this.numero;
					this.resultado = this.inmediato(n);
					this.$swal.fire({
						position: 'top-end',
						icon: 'success',
						title: 'La petición se completo correctamente',
						showConfirmButton: false,
						timer: 1500,
					});
				}
			});
		}
	}

	public fib(n: any): any {
		if (n < 2) {
			return n;
		}
		return this.fib(n - 1) + this.fib (n - 2);
	}

	public inmediato(n: any) {
		let i = 0;
		let temp;
		let res;
		while (i <= n) {
			temp = this.fib(i);
			if (temp <= n) {
				res = temp;
			}
			i++;
		}
		return res;
	}

}
</script>