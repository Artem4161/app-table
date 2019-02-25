<template>
	<td v-if="indexCell !== 'id'" class="table__cell">
		<div class="table__cell-wrap">
			<span class="table__input-wrap">
				<input class="table__input table__input--hoshi" type="text" 
					:value="item"
					@input="onInput">
				<label class="table__label table__label--hoshi"></label>
				<span class="table__btn">
					<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
					 width="12px" height="12px" viewBox="0 0 540.329 540.329" style="enable-background:new 0 0 540.329 540.329;"
					 xml:space="preserve">
						<g>
							<g>
								<polygon points="0.002,540.329 58.797,532.66 7.664,481.528 		"/>
								<polygon points="16.685,412.341 10.657,458.56 81.765,529.668 127.983,523.64 442.637,208.992 331.338,97.688 		"/>
								<path d="M451.248,5.606C447.502,1.861,442.57,0,437.57,0c-5.264,0-10.6,2.062-14.701,6.157L346.92,82.106l111.299,111.298
									l75.949-75.949c7.992-7.986,8.236-20.698,0.557-28.378L451.248,5.606z"/>
							</g>
						</g>
					</svg>
				</span>
			</span>
		</div>
	</td>
</template>

<script>

export default {
	props: ['item', 'indexCell'], 
	methods: {
		onInput(e) {
			this.$emit('change', e.target.value);
		}
	}
};
</script>

<style lang="sass">

.table__cell
	position: relative
	font-size: 14px
	padding: 15px 10px
	vertical-align: middle

.table__cell:nth-child(2)
	min-width: 200px

.table__cell:first-child
	padding: 15px 10px 15px 20px

.table__cell:last-child
	padding: 15px 20px 15px 10px

.table__cell-wrap
	position: relative
	width: 100%
		
.table__btn
	position: absolute
	top: 5px
	right: 0px
	fill: rgba(0,0,0,.3)
	transition: .3s
	background: transparent
	opacity: 0
	z-index: 1

.table__cell:hover
	.table__btn
		opacity: 1

.table__input
	font-family: 'robotolight'
	color: #000
	font-size: 14px
	width: calc(100% - 18px)
	height: 14px
	padding: 4px 0
	border: none

.table__input:focus ~ .table__btn
	fill: rgba(0,0,0,.8)
	opacity: 1

.table__label--hoshi
	bottom: -7px
	height: 100%

.table__input-wrap
	position: relative
	width: 100%
	z-index: 1
	vertical-align: top
	overflow: hidden

.table__input--hoshi
	position: relative
  	display: block
  	border: none
  	border-radius: 0
  	color: #aaa
  	background: transparent
  	-webkit-appearance: none

.table__input--hoshi:focus
    outline: none

.table__label--hoshi
    position: absolute
    bottom: -6px
    left: 0
    width: 100%
    height: 100%
    text-align: left
    pointer-events: none

.table__label--hoshi
    &::before
        content: ''
        position: absolute
        top: 0
        left: 0
        width: 100%
        height: calc(100% - 8px)
    &::after
    	content: ''
    	position: absolute
    	top: 0
    	left: 0
    	width: 100%
    	height: calc(100% - 8px)
    	border-bottom: 1px solid #B9C1CA
    	border-bottom: 2px solid red
    	-webkit-transform: translate3d(-100%, 0, 0)
    	transform: translate3d(-100%, 0, 0)
    	-webkit-transition: -webkit-transform 0.3s
    	transition: transform 0.3s

.table__label--hoshi::after
  	border-color: hsl(200, 100%, 50%)


.table__input--hoshi:focus + .table__label--hoshi::after
    -webkit-transform: translate3d(0, 0, 0)
    transform: translate3d(0, 0, 0)

@-webkit-keyframes anim-1
  50%
    opacity: 0
    -webkit-transform: translate3d(1em, 0, 0)
    transform: translate3d(1em, 0, 0)

  51%
    opacity: 0
    -webkit-transform: translate3d(-1em, -40%, 0)
    transform: translate3d(-1em, -40%, 0)

  100%
    opacity: 1
    -webkit-transform: translate3d(0, -40%, 0)
    transform: translate3d(0, -40%, 0)


@keyframes anim-1
  50%
    opacity: 0
    -webkit-transform: translate3d(1em, 0, 0)
    transform: translate3d(1em, 0, 0)

  51%
    opacity: 0
    -webkit-transform: translate3d(-1em, -40%, 0)
    transform: translate3d(-1em, -40%, 0)

  100%
    opacity: 1
    -webkit-transform: translate3d(0, -40%, 0)
    transform: translate3d(0, -40%, 0)


</style>