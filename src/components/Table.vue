<template>
	<div class="table-wrap">
		<table class="table">
	        <app-table-head 
	        	:titles="titles"
	        	:sortParam="sortParam"
	        	:sortParamDir="sortParamDir"
	        	@change="onSort">
	        </app-table-head>
	        <tr v-for="(row, indexRow) in showItems" 
	            :key="indexRow">
	            <app-table-cell v-for="(item, indexCell) in row" 
	                :key="indexCell" 
	                :item="item"
	                @change="onChange(indexRow, indexCell, $event)">  
	            </app-table-cell>
	        </tr>
	    </table>
	    <app-pagination
	    	v-if="!hidePagination"
	        :currentPage="currentPage"
	        :totalItems="totalItems"
	        @changedPage="onChangedPage"  
	        @changedPerPage="onChangedPerPage">  
	    </app-pagination>
	</div>
</template>

<script>
import AppTableHead from './TableHead.vue';
import AppTableCell from './TableCell.vue';
import AppPagination from './Pagination.vue';

export default {
	props: {
		titles: {
	      type: Object,
	      required: true
	    },
	    items: {
	      type: Array,
	      required: true
	    }
	},
	components: {
		AppTableHead,
		AppTableCell,
		AppPagination
	},
	data() {
		return {
			currentPage: 1,
            perPage: 8,
			sortParam: '',
			sortParamDir: ''
		}
	},
	computed: {
		totalItems() {
            return this.items.length;
        },
        showItems() {
        	return this.items.slice(this.showFromto, this.showUpto);
        },
        showFromto() {
            return this.perPage != 1 ? (this.currentPage * this.perPage) - this.perPage : 0;
        },
        showUpto() {
            return this.currentPage * this.perPage;
        },
        hidePagination() {
        	return this.showItems.length < this.perPage && this.currentPage == 1;
        }
	},
	methods: {
		onSort({title}) {
			this.sortParam = title.toLowerCase();
			this.sortParamDir = this.sortParamDir == 'asc' ? 'desc' : 'asc';

			this.items.sort((a,b) => {
				let modifier = 1;
				if(this.sortParamDir === 'desc') modifier = -1;
				if(a[this.sortParam] < b[this.sortParam]) return -1 * modifier;
				if(a[this.sortParam] > b[this.sortParam]) return 1 * modifier;
				return 0;
			})
		},
		onChange(indexRow, indexCell, value) {
			this.$emit('change', {
				indexRow: indexRow,
				indexCell: indexCell,
                value: value
            });
		},
		onChangedPage(page) {
            this.currentPage = page;
        },
        onChangedPerPage(perPage) {
        	this.perPage = perPage;
        }
	}
};
</script>

<style lang="sass" scoped>

.table
    font-size: 14px
    width: 100%
    background: #fff
    th, td 
        border-bottom: solid 1px #e0e0e0
        text-align: left

</style>

