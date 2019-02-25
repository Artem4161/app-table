<template>
	<div class="data-table">
		<app-search
	        @search="onSearch($event)">   
	    </app-search>
        
        <transition name="fade">
            <app-selected-items
                v-show="selectedRowsLength"
                :selectedItems="selectedRowsLength"
                @remove="onRemove">
            </app-selected-items>
        </transition>

 	    <app-table
	        v-show="filteredData.length"
	        :titles="titles"
	        :items="filteredData"
            :perPage="perPage"
            :selectedRows="selectedRows"
	        @change="onChange"
            @select="getSelectedRows">
	    </app-table>

	    <app-no-result
	        v-show="!filteredData.length">
	    </app-no-result>
	</div>
</template>

<script>
import AppSearch from './Search.vue';
import AppSelectedItems from './SelectedItems.vue';
import AppTable from './Table.vue';
import AppNoResult from './NoResult.vue';

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
	    }
	},
	components: {
        AppSearch,
        AppSelectedItems,
        AppTable,
        AppNoResult
    },
    data() {
    	return {
    		currentItems: this.items,
    		search: '',
    		filteredData: [],
            selectedRows: []
    	}
    },
    computed: {
        selectedRowsLength() {
            return this.selectedRows.length;
        }
    },
    methods: {
        onSearch(e) {
            this.search = e.value;
            this.getfilteredData();
        },
        getfilteredData() {
            this.filteredData = this.currentItems;
            let search = this.search.toLowerCase();

            if (search) {
                const filterFields = Object.keys(this.currentItems[0]);

                this.filteredData = this.filteredData.filter(item => {
                    return filterFields.some(field => String(item[field]).toLowerCase().indexOf(search) > -1);
                });
            }
        },
        onChange({indexRow, indexCell, value}) {
            this.currentItems[indexRow][indexCell] = value;
        },
        getSelectedRows(rows) {
            this.selectedRows = rows;
        }, 
        onRemove() {
            for(var i = 0; i < this.currentItems.length; i++) {
                var obj = this.currentItems[i];

                if(this.selectedRows.indexOf(obj.name) !== -1) {
                    this.currentItems.splice(i, 1);
                    i--;
                }
            }

            this.selectedRows = [];
        }
    },
    mounted() {
        this.getfilteredData();
    }
};
</script>

<style lang="sass">

.data-table
    background: #fff
    box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 1px 5px 0 rgba(0, 0, 0, 0.12), 0 3px 1px -2px rgba(0, 0, 0, 0.2)
    border-radius: 2px

</style>