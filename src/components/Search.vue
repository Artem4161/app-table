<template>
	<form class="search">
		<span class="search-wrap">
			<input class="search__input input__field input__field--hoshi" 
                type="text" 
                placeholder="Search"
                @input="onSearch">
			<label class="input__label input__label--hoshi input__label--hoshi-color-1"></label>
			<span class="search__submit">
				<svg class="search-ic" width="16" height="16" viewBox="0 0 18 18" fill="rgba(0,0,0,.6)" xmlns="http://www.w3.org/2000/svg">
					<path d="M12.5 11H11.71L11.43 10.73C12.41 9.59 13 8.11 13 6.5C13 2.91 10.09 0 6.5 0C2.91 0 0 2.91 0 6.5C0 10.09 2.91 13 6.5 13C8.11 13 9.59 12.41 10.73 11.43L11 11.71V12.5L16 17.49L17.49 16L12.5 11ZM6.5 11C4.01 11 2 8.99 2 6.5C2 4.01 4.01 2 6.5 2C8.99 2 11 4.01 11 6.5C11 8.99 8.99 11 6.5 11Z"/>
				</svg>
			</span>	        
		</span>
    </form>
</template>

<script>
export default {
	methods: {
        onSearch(e) {
            this.$emit('search', {
                value: e.target.value
            });
        }
    }
};
</script>

<style lang="sass" scoped>

.search
	position: relative
	padding: 15px 30px
	background: #fff

.search__input
	width: 200px
	padding: 15px 15px 15px 28px
	font-family: 'robotolight'
	color: #000

.search__submit
	position: absolute
	top: 16px
	left: 2px
	border: none
	width: 17px
    height: 17px
	background: transparent
	z-index: 1
	fill: rgba(0,0,0,.4)
	padding: 0

.search-wrap
	position: relative
    z-index: 1
    display: inline-block
    vertical-align: top
	overflow: hidden 

.input__field
    position: relative
    display: block
    border: none
    border-radius: 0
    background: #f0f0f0
    color: #aaa
    -webkit-appearance: none
    &:focus
    	outline: none

.input__field--hoshi
  	background: transparent
  	color: #595F6E

.input__label--hoshi
    position: absolute
    bottom: 0
    left: 0
    width: 100%
    height: calc(100% - 1em)
    text-align: left
    pointer-events: none

.input__label-content--hoshi
  	position: absolute

.input__label--hoshi
    &::before
        content: ''
        position: absolute
        top: 0
        left: 0
        width: 100%
        height: calc(100% - 8px)
        border-bottom: 1px solid #B9C1CA
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

.input__label--hoshi-color-1::after
  	border-color: hsl(200, 100%, 50%)

.input__field--hoshi:focus + .input__label--hoshi::after, .input--filled .input__label--hoshi::after
	-webkit-transform: translate3d(0, 0, 0)
	transform: translate3d(0, 0, 0)

.input__field--hoshi:focus + .input__label--hoshi .input__label-content--hoshi
    -webkit-animation: anim-1 0.3s forwards
    animation: anim-1 0.3s forwards

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