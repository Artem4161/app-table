<template>
	<div class="pagination-wrap">
		<div class="pagination">
			<ul>
				<li @click="changePage(1)" 
					:class="{ disabled: hasPrev }">
					<span class="pagination__first">
						<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="12px" height="12px" x="0px" y="0px" viewBox="0 0 192.701 192.701" style="enable-background:new 0 0 192.701 192.701;" xml:space="preserve">
							<g>
								<g id="Double_Chevron_Left">
									<path d="M29.641,96.345l74.54-75.61c4.704-4.74,4.704-12.439,0-17.179c-4.704-4.74-12.319-4.74-17.011,0l-82.997,84.2
										c-4.511,4.559-4.535,12.608,0,17.191l83.009,84.2c4.692,4.74,12.319,4.74,17.011,0c4.704-4.74,4.704-12.439,0-17.179
										L29.641,96.345z"/>
									<path d="M113.853,96.345l74.54-75.61c4.704-4.74,4.704-12.439,0-17.179c-4.704-4.74-12.319-4.74-17.011,0l-82.997,84.2
										c-4.511,4.559-4.535,12.608,0,17.191l82.997,84.2c4.704,4.74,12.319,4.74,17.011,0c4.704-4.74,4.704-12.439,0-17.179
										L113.853,96.345z"/>
								</g>
							</g>
						</svg>
					</span>
				</li>
				<li @click="changePage(prevPage)" 
					:class="{ disabled: hasPrev }">
					<span class="pagination__prev">
						<svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="12px" height="12px" x="0px" y="0px" viewBox="0 0 240.823 240.823" style="enable-background:new 0 0 240.823 240.823;" xml:space="preserve">
							<path id="Chevron_Right" d="M57.633,129.007L165.93,237.268c4.752,4.74,12.451,4.74,17.215,0c4.752-4.74,4.752-12.439,0-17.179
								l-99.707-99.671l99.695-99.671c4.752-4.74,4.752-12.439,0-17.191c-4.752-4.74-12.463-4.74-17.215,0L57.621,111.816
								C52.942,116.507,52.942,124.327,57.633,129.007z"/>
						</svg>
					</span>
				</li>
				<li><span class="pagination__pages">{{ currentPage }} of {{ totalPage }}</span></li>
				<li @click="changePage(nextPage)"
					:class="{ disabled: hasNext }">
					<span class="pagination__next">
						<svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="12px" height="12px" x="0px" y="0px" viewBox="0 0 240.823 240.823" style="enable-background:new 0 0 240.823 240.823;" xml:space="preserve">
							<path id="Chevron_Right_1_" d="M183.189,111.816L74.892,3.555c-4.752-4.74-12.451-4.74-17.215,0c-4.752,4.74-4.752,12.439,0,17.179
								l99.707,99.671l-99.695,99.671c-4.752,4.74-4.752,12.439,0,17.191c4.752,4.74,12.463,4.74,17.215,0l108.297-108.261
								C187.881,124.315,187.881,116.495,183.189,111.816z"/>
						</svg>
					</span>
				</li>
				<li @click="changePage(totalPage)"
					:class="{ disabled: hasNext }">
					<span class="pagination__last">
						<svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="12px" height="12px" x="0px" y="0px" viewBox="0 0 192.689 192.689" style="enable-background:new 0 0 192.689 192.689;" xml:space="preserve">
							<g>
								<g id="Double_Chevron_Right">
									<path d="M188.527,87.755l-83.009-84.2c-4.692-4.74-12.319-4.74-17.011,0c-4.704,4.74-4.704,12.439,0,17.179l74.54,75.61
										l-74.54,75.61c-4.704,4.74-4.704,12.439,0,17.179c4.704,4.74,12.319,4.74,17.011,0l82.997-84.2
										C193.05,100.375,193.062,92.327,188.527,87.755z"/>
									<path d="M104.315,87.755l-82.997-84.2c-4.704-4.74-12.319-4.74-17.011,0c-4.704,4.74-4.704,12.439,0,17.179l74.528,75.61
										l-74.54,75.61c-4.704,4.74-4.704,12.439,0,17.179s12.319,4.74,17.011,0l82.997-84.2C108.838,100.375,108.85,92.327,104.315,87.755
										z"/>
								</g>
							</g>
						</svg>
					</span>
				</li>
			</ul>
 		</div>
 		<div class="pagination__select-wrap">
 			<span>Rows per page:</span>
 			<select class="pagination__select"
				@change="onSelectPerPage"
				v-model="currentPerPage">
			    <option value="5">5</option>
			    <option value="8">8</option>
			    <option value="10">10</option>
			    <option value="20">20</option>
			</select>
 		</div>
		
	</div>
</template>

<script>
	
export default {
	props: {
		currentPage: {
			type: Number,
			default: 1
		},
		totalItems: {
			type: Number,
			default: 0
		},
		perPage: {
			type: Number,
			default: 10
		}
	},
	data() {
		return {
			currentPerPage: this.perPage
		}
	},
	computed: {
		pages() {
			let pages = [];

			for (let i = this.rangeStart; i <= this.rangeEnd; i++) {
				pages.push(i);
			}

			return pages;
		},
		nextPage() {
			let nextPage = this.currentPage + 1;

			if (nextPage >= this.totalPage) {
				nextPage = this.totalPage
			}

			return nextPage;
		},
		prevPage() {
			let prevPage = this.currentPage - 1;

			if (prevPage <= 1) {
				prevPage = 1
			}

			return prevPage;	
		},
		hasPrev(){
			return this.currentPage <= 1;
		},
		hasNext(){
			return this.currentPage >= this.totalPage;
		},
		hasFirst() {
			return this.rangeStart !== 1;
		},
		hasLast() {
			return this.rangeEnd < this.totalPage;
		},
		totalPage() {
			return Math.ceil(this.totalItems / this.perPage);
		}
	},
	methods: {
		changePage(page) {
			this.$emit('changedPage', page);
		},
		onSelectPerPage(e) {
			this.$emit('changedPerPage', {
				perPage: e.target.value,
				page: 1
			});		
		}
	}
};
</script>

<style lang="sass">

.pagination-wrap
	position: relative
	text-align: center
	padding: 20px
	font-family: 'robotolight'
	font-size: 14px

.pagination
	li
		display: inline-block
		span
			padding: 10px
			cursor: pointer
			margin: 0 5px
			transition: 0.3s
			opacity: .7
		span.pagination__pages
			font-family: 'robotoregular'
			font-size: 14px
			cursor: default
			opacity: 1
			color: rgba(0,0,0,.6)
		span:hover
			opacity: 1
	li.disabled
		span 
			opacity: .2
			cursor: default

.pagination__select-wrap
	position: absolute
	top: 25px
	left: 25px
	font-size: 14px
	color: rgba(0,0,0,.8)
	span
		margin-right: 10px
		padding-top: 4px

.pagination__select
	border: solid 1px transparent
	color: rgba(0,0,0,.8)
	font-family: 'robotolight'
	font-size: 14px
	vertical-align: top

</style>