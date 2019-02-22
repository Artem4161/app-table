<template>
	<div class="pagination-wrap">
		<ul class="pagination">
			<li v-if="hasPrev" @click="changePage(prevPage)"><span class="pagination__left">Prev</span></li>
			<li v-if="hasFirst" @click="changePage(1)"><span>1</span></li>
			<li v-if="hasFirst">...</li>
			<li v-for="page in pages"
				:class="{ current: currentPage == page }"
				@click="changePage(page)">
				<span>{{ page }}</span>
			</li>
			<li v-if="hasLast">...</li>
			<li v-if="hasLast" @click="changePage(totalPage)"><span>{{ this.totalPage }}</span></li>
			<li v-if="hasNext" @click="changePage(nextPage)"><span class="pagination__left">Next</span></li>
		</ul>
		<select class="pagination__select"
			@click="onSelectPerPage"
			v-model="perPage">
		    <option value="5">Show by 5</option>
		    <option value="8">Show by 8</option>
		    <option value="10">Show by 10</option>
		    <option value="20">Show by 20</option>
		</select>
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
		pageRange: {
			type: Number,
			default: 2
		}
	},
	data() {
		return {
			perPage: 8
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
		rangeStart(){
			let start = this.currentPage - this.pageRange;

			return (start > 0) ? start : 1;
		},
		rangeEnd(){
			let end = this.currentPage + this.pageRange;

			return (end < this.totalPage) ? end : this.totalPage;
		},
		nextPage() {
			return this.currentPage + 1;
		},
		prevPage() {
			return this.currentPage - 1;	
		},
		hasPrev(){
			return this.currentPage > 1;
		},
		hasNext(){
			return this.currentPage < this.totalPage;
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
			this.$emit('changedPerPage', e.target.value);
		}
	}
};
</script>

<style lang="sass" scoped>

.pagination-wrap
	position: relative
	text-align: center
	padding: 20px
	font-family: 'robotolight'
	font-size: 14px
.pagination
	li
		display: inline-block
		padding: 10px 15px
		cursor: pointer
		border: solid 1px #e0e0e0
		border-radius: 2px
		margin: 0 5px
		transition: 0.3s
	li:hover
		border: solid 1px hsl(200, 100%, 50%)
	li.current
		color: hsl(200, 100%, 50%)
		border: solid 1px hsl(200, 100%, 50%)
		font-family: 'robotoregular'
.pagination__select
	position: absolute
	top: 15px
	left: 15px
	font-family: 'robotolight'
	border: solid 1px #e0e0e0
	font-size: 14px
	padding: 8px

</style>