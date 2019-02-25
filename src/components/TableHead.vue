<template>
	<tr>
		<th></th>
		<th v-for="(title, key) in titles"
			:key="key"
			class="table__caption"
			:class="key === sortParam ? sortParamDir : ''"
			@click="onChange(key)">
			<span class="table__caption-wrap">
				<svg version="1.1" class="arrow-ic" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="12px" height="12px" viewBox="0 0 408 408" style="enable-background:new 0 0 408 408;" xml:space="preserve">
					<g>
						<g id="arrow-back">
							<path d="M408,178.5H96.9L239.7,35.7L204,0L0,204l204,204l35.7-35.7L96.9,229.5H408V178.5z"/>
						</g>
					</g>
				</svg>
				{{title}}
			</span>
		</th>
	</tr>
</template>

<script>

export default {
	props: {
		titles: {
	        type: Object,
	        required: true
	    },
	    sortParam: {
	        type: String,
	        required: false
	    },
	    sortParamDir: {
	        type: String,
	        required: false
	    }
	},
	methods: {
		onChange(title) {    
			this.$emit('change', {
				title: title,
				page: 1
			});
		}
	}
};
</script>

<style lang="sass">

.table__caption
	font-size: 14px
	padding: 15px
	cursor: pointer
	text-align: left
	border-bottom: solid 1px #e0e0e0

.table__caption:nth-child(2)
	// padding: 15px 15px 15px 30px

.table__caption:hover
	.table__caption-wrap
		color: rgba(0,0,0,1)
		.arrow-ic
    		opacity: 1
    		
.table__caption-wrap
    position: relative
    font-family: 'robotoregular'
    color: rgba(0,0,0,.54)
    transition: .3s
    .arrow-ic
        position: absolute
        top: 1px
        left: -18px
        transform: rotate(-90deg)
        opacity: 0
        fill: rgba(0,0,0,.2)
        transition: .3s

.table__caption.asc
	.table__caption-wrap
		color: rgba(0,0,0,1)
		.arrow-ic
	        transform: rotate(90deg)
	        fill: rgba(0,0,0,1)
	        opacity: 1

.table__caption.desc
	.table__caption-wrap
		color: rgba(0,0,0,1)
		.arrow-ic
	        transform: rotate(-90deg)
	        fill: rgba(0,0,0,1)
	        opacity: 1

</style>