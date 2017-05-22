<template>
	<button class='v-button' v-bind:class='[{disabled: disabled}, cssClasses]' @click='onClickHandler' :disabled='disabled'>
		<slot v-if='!disabled'>button</slot>
		<slot v-else>...</slot>
	</button>
</template>

<script>
export default {
  props: {
    onClick: {
      type: Function,
      required: true,
  	},
	cssClasses: {
	  type: String,
	  required: false,
    },
	disabled: {
		type: Boolean,
		required: false,
		default: false,
	},
	spamable: {
		type: Boolean,
		required: false,
		default: false,
	},
	cooldown: {
		type: String,
		required: false,
        default: '300',
	},
  },
  computed: {
	isSpamable(){
	  return this.spamable === 'true';
	},
	isDisabled(){
	  return this.disabled === 'true' || this.disabled === true;
    },
  },
  methods: {
	onClickHandler(){
	  if (this.spamable) {
		this.onClick(this);
	  } else {
		this.disabled = true;
	  	this.onClick(this);
	  	setTimeout(() => {
	  	  this.disabled = false;
	  	}, this.cooldown);
	  }
	},
  },
};
</script>

<style lang="scss" scoped>
.v-button {
	display: inline-block;
	height: 32px;
	line-height: 32px;
	text-align: center;
	cursor: pointer;
	background-color: rgb(30, 180, 160);
	color: rgb(255, 255, 255);
	border: none;
	border-radius: 5px;
	min-width: 160px;
	&:hover {
		background-color:rgb(40, 190, 190);
	}
	&.disabled {
		background-color: rgb(230, 230, 230);
	}
}
</style>
