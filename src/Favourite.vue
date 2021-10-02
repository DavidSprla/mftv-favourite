<template>
	<div class="movies" :class="{'movies--inspect': inspect}">
		<div class="movies__container">
			<h1 class="movies__title">
				Favourite
			</h1>
			<div v-if="movies.length !== 0" class="movies__grid">
				<div v-for="movie in movies" :key="movie.id" class="movies__item">
					<div class="movies__background"></div>
					<button type="button" class="movies__favourite" :class="{'movies__favourite--active': movie.favourite}">
						<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve" class="movies__favourite-icon">
							<path d="M376,30c-27.783,0-53.255,8.804-75.707,26.168c-21.525,16.647-35.856,37.85-44.293,53.268    c-8.437-15.419-22.768-36.621-44.293-53.268C189.255,38.804,163.783,30,136,30C58.468,30,0,93.417,0,177.514    c0,90.854,72.943,153.015,183.369,247.118c18.752,15.981,40.007,34.095,62.099,53.414C248.38,480.596,252.12,482,256,482    s7.62-1.404,10.532-3.953c22.094-19.322,43.348-37.435,62.111-53.425C439.057,330.529,512,268.368,512,177.514    C512,93.417,453.532,30,376,30z"/>
						</svg>
					</button>
					<div class="movies__info">
						<div class="movies__name">
							{{ movie.title }}
						</div>
					</div>
				</div>
			</div>
			<div v-else class="movies__empty">
				Favourite list is empty
			</div>
		</div>
  </div>
</template>

<script>
export default {
  name: 'Favourite',
  data: () => ({
		inspect: false,
    movies: JSON.parse(localStorage.getItem("movies")) || []
  }),
	methods: {
		handleInspect(event) {
			this.inspect = event.detail 
		}
	},
	mounted() {
		window.addEventListener('inspectEvent', this.handleInspect)

		const inspectStorage = JSON.parse(localStorage.getItem('inspect')) || false
		this.inspect = inspectStorage
	},
	destroyed() {
		window.removeEventListener('inspectEvent', this.handleInspect)
	}
}
</script>

<style scoped>
	.movies{
		position: relative;
		margin: 3rem 1.5rem;
		transition: var(--transition);
	}
	.movies--inspect{
		padding-top: 3rem;
		border-radius: 1rem;
		box-shadow: 0 0 .6rem .1rem var(--vue);
	}
	.movies--inspect::before{
		position: absolute;
		content: 'favourite (Vue)';
		top: 1rem;
		left: 1.5rem;
		color: var(--vue);
	}
	.movies__container{
		max-width: 160rem;
		padding: 1.5rem;
		margin: 0 auto;
	}
	.movies__title{
		margin: 0;
		padding-bottom: 1rem;
		font-size: 4rem;
		font-weight: 700;
		color: var(--dark-gray);
		letter-spacing: .02em;
		text-transform: uppercase;
		text-align: center;
		user-select: none;
		cursor: default;
	}
	@media only screen and (min-width: 768px) {
		.movies__title{
			text-align: left;
		}
	}
	.movies__grid{
		display: grid;
		grid-template-columns: repeat(1, 1fr);
		row-gap: 1rem;
	}
	@media only screen and (min-width: 425px) {
		.movies__grid{
			grid-template-columns: repeat(2, 1fr);
			column-gap: 1rem;
		}
	}
	@media only screen and (min-width: 768px) {
		.movies__grid{
			grid-template-columns: repeat(3, 1fr);
			column-gap: 3rem;
			row-gap: 3rem;
		}
	}
	@media only screen and (min-width: 1024px) {
		.movies__grid{
			grid-template-columns: repeat(4, 1fr);
		}
	}
	@media only screen and (min-width: 1440px) {
		.movies__grid{
			grid-template-columns: repeat(5, 1fr);
		}
	}
	.movies__item{
		position: relative;
		min-height: 20rem;
		padding: 1rem;
		border-radius: 1rem;
		overflow: hidden;
		transition: var(--transition);
	}
	.movies__item:hover{
		box-shadow: 0 0 1rem var(--gray);
	}
	.movies__background{
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-image: url("https://picsum.photos/id/184/400/300");
		background-repeat: no-repeat;
		background-position: bottom;
		border-radius: 1rem;
	}
	.movies__favourite{
		position: absolute;
		top: 1rem;
		right: 1rem;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: .6rem;
		background: rgba(0,0,0,0.5);
		border-radius: 50%;
		box-shadow: none;
		border: none;
		cursor: default;
		outline: none;
	}
	.movies__favourite--active .movies__favourite-icon{
		fill: var(--red);
	}
	.movies__favourite-icon{
		fill: var(--light-gray);
		width: 1.8rem;
		height: 1.8rem;
	}
	.movies__info{
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 1.5rem 1rem;
		background: rgba(0,0,0,0.5);
		user-select: none;
	}
	.movies__name{
		font-weight: 500;
		color: var(--white);
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.movies__empty{
		padding: 6rem 0;
		text-align: center;
		font-size: 2.6rem;
		font-weight: 500;
		color: var(--dark-gray);
	}
</style>
