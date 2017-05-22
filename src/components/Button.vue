<template>
	<button class='v-button' v-bind:class='[{disabled: isDisabled}, cssClasses]' @click='onClickHandler' :disabled='isDisabled'>
		<slot v-if='!isDisabled'>button</slot>
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
		type: String,
		required: false,
		default: 'false',
	},
	spamable: {
		type: String,
		required: false,
		default: 'false',
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
	  if (this.isSpamable) {
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
  /*data() {
	return {
	  isActive: disabled || false,
	  debugger;
  	};
},*/
};
</script>

<style lang="scss" scoped>
.v-button {
	margin-right: .333%;
	margin-top: .333%;
	float: left;
	display: inline-block;
	width: 33%;
	height: 50px;
	line-height: 50px;
	text-align: center;
	cursor: pointer;
	background-color: rgb(240, 240, 240);
	color: rgb(58, 57, 74);
	border: none;
	&:hover {
		background-color: rgb(245, 245, 245);
	}
	&.disabled {
		background-color: rgb(230, 230, 230);
	}
}
</style>
