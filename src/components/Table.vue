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

	            <td class="table__cell">
	            	<input type="checkbox"
	            	class="checkbox" 
	            		:value="indexRow"
	            		v-model="currentSelectedRows"
	            		@change="onSelect">
	            	<span class="checkbox-span"><svg version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 26 26" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#fff" enable-background="new 0 0 26 26">
					  <path d="m.3,14c-0.2-0.2-0.3-0.5-0.3-0.7s0.1-0.5 0.3-0.7l1.4-1.4c0.4-0.4 1-0.4 1.4,0l.1,.1 5.5,5.9c0.2,0.2 0.5,0.2 0.7,0l13.4-13.9h0.1v-8.88178e-16c0.4-0.4 1-0.4 1.4,0l1.4,1.4c0.4,0.4 0.4,1 0,1.4l0,0-16,16.6c-0.2,0.2-0.4,0.3-0.7,0.3-0.3,0-0.5-0.1-0.7-0.3l-7.8-8.4-.2-.3z"/>
					</svg></span>
	            </td>

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
	        :perPage="currentPerPage"
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
	    },
	    perPage: {
	    	type: Number,
	    	default: 10
	    },
	    selectedRows: Array
	},
	components: {
		AppTableHead,
		AppTableCell,
		AppPagination
	},
	data() {
		return {
			currentPage: 1,
            currentPerPage: this.perPage,
			sortParam: '',
			sortParamDir: '',
			currentSelectedRows: this.selectedRows
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
            return this.currentPerPage != 1 ? (this.currentPage * this.currentPerPage) - this.currentPerPage : 0;
        },
        showUpto() {
            return this.currentPage * this.currentPerPage;
        },
        hidePagination() {
        	return this.showItems.length < this.currentPerPage && this.currentPage == 1;
        }
	},
	methods: {
		onSort({title, page}) {
			this.currentPage = page;
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
        onChangedPerPage({perPage, page}) {
        	this.currentPerPage = Number(perPage);
        	this.currentPage = page;
        },
        onSelect() {
        	this.$emit('select', this.currentSelectedRows);

        }
	},
	watch: {
		selectedRows() {
			this.currentSelectedRows = this.selectedRows;
		}
	}
};
</script>

<style lang="sass">

.table
    font-size: 14px
    width: 100%
    background: #fff
    th, td 
        border-bottom: solid 1px #e0e0e0
        text-align: left

.checkbox
	position: absolute
	top: 18px
	left: 20px
	width: 18px
	height: 18px
	opacity: 0
	cursor: pointer

.checkbox-span
	width: 12px
	height: 12px
	border-radius: 2px
	border: solid 2px rgba(0,0,0,.8)
	cursor: pointer
	transition: .3s

.checkbox:checked + .checkbox-span
    background: #ff4081
    border: solid 2px #ff4081


</style>

