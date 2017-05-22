<template>
	<button :class="['button', {'disabled': btnDisabled}, cssClasses]" @click='onClickHandler' :disabled='btnDisabled'>
		<main v-if='!btnDisabled'>
			<slot>button</slot>
		</main>
		<main v-else>
			<slot name="disabled">...</slot>
		</main>

	</button>
</template>

<script>
export default {
  name: 'button',
  props: {
    onClick: {
      type: Function,
      required: false,
	  default: () => {
		  return new Function();
	  }
  	},
	cssClasses: { //TODO add limit to only accept acknoledged css classes
	  type: String,
	  required: false,
    },
	disabled: {
		type: Boolean,
		required: false,
		default: false,
	},
	throttled: {
		type: Boolean,
		required: false,
		default: false,
	},
	cooldown: {
		type: Number,
		required: false,
        default: 300,
	},
	size: { //TODO add support for predefined sizes.
		type: String,
		required: false,
		default: "1em"
	},
  },
  methods: {
	onClickHandler(){
	  if (!this.throttled) {
		this.onClick(this);
	  } else {
		this.btnDisabled = true;
	  	this.onClick(this);
	  	setTimeout(() => {
	  	  this.btnDisabled = false;
	  	}, this.cooldown);
	  }
	},
  },
  data(){
	return {
		btnDisabled: this.disabled
	}
  },
};
</script>

<style lang="scss" scoped>
$border-radius: 5px;
$base-size: 32px;
$base-color: #333;
$base-padding: 20px;
$base-font-size: 1em;
$base-line-height: (1.2 * $base-font-size);
$disabled-bg: lighten($base-color, 75%);
$disabled-text: lighten($base-color, 25%);
$btn-text-dark: #333;
$btn-text-light: #eee;

$btn-default-bg: rgb(230, 230, 230);
$btn-primary-bg: rgb(45, 112, 172);
$btn-success-bg: rgb(54, 156, 74);
$btn-info-bg: rgb(67, 173, 191);
$btn-warning-bg: rgb(210, 165, 77);
$btn-danger-bg: rgb(173, 29, 64);
$btn-link-bg: transparent;

.button {
	display: inline-block;
	font-size: $base-font-size;
	line-height: $base-line-height;
	text-align: center;
	border: none;
	border-radius: $border-radius;
	min-width: 160px;
	cursor: pointer;
	padding:($base-padding / 2) $base-padding;
	background-color: $btn-default-bg;
	color: $btn-text-dark;
	-webkit-transition: all .4s;
	transition: all .4s;
	box-shadow: 0 1px 0px 0 rgba(0,0,0,0.1);
	&:hover {
		background-color:lighten($btn-default-bg, 5%);
		box-shadow: 0 1px 3px 0 rgba(0,0,0,0.3);
	}
	&.primary {
	background-color: $btn-primary-bg;
	color:$btn-text-light;
		&:hover {
			background-color:lighten($btn-primary-bg, 5%);
		}
	}
	&.success {
		background-color: $btn-success-bg;
		color:$btn-text-light;
		&:hover {
			background-color:lighten($btn-success-bg, 5%);
		}
	}
	&.info {
		background-color: $btn-info-bg;
		color:$btn-text-light;
		&:hover {
			background-color:lighten($btn-info-bg, 5%);
		}
	}
	&.warning {
		background-color: $btn-warning-bg;
		color:$btn-text-light;
		&:hover {
			background-color:lighten($btn-warning-bg, 5%);
		}
	}
	&.danger {
		background-color: $btn-danger-bg;
		color:$btn-text-light;
		&:hover {
			background-color:lighten($btn-danger-bg, 5%);
		}
	}
	&.link {
		background-color: $btn-link-bg;
		color:$btn-primary-bg;
		&:hover {
			color:lighten($btn-primary-bg, 5%);
		}
	}
	&.disabled {
		background-color: $disabled-bg;
		color: $disabled-text;
		cursor: default;
		&:hover {
			background-color: $disabled-bg;
			color: $disabled-text;
			box-shadow: none;
		}
	}
}
</style>
