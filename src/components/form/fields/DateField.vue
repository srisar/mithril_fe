<template>
	
	
	<div class="form-control w-full">
		<label class="label">
			<span class="label-text">
				<slot name="label"></slot>
				<span v-if="required" class="text-error">*</span>
			</span>
		</label>
		<Datepicker
			v-model="modelData"
			format="yyyy-MM-dd"
			auto-apply
			:clearable="false"
			:enable-time-picker="false"
		/>
		<label class="label">
			<span class="label-text-alt">
				<slot name="footer"></slot>
			</span>
		</label>
	</div>

</template>

<script setup lang="ts">
import {ref, reactive, computed} from 'vue';
import Datepicker from '@vuepic/vue-datepicker';
import dayjs from 'dayjs';


/* ------------------------------------------------------------------------------------------------------------------ */
/* region Props */

interface Props {
	modelValue?: dayjs.Dayjs;
	invalid?: boolean;
	required?: boolean;
	readonly?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
	modelValue: () => dayjs()
});

const emits = defineEmits(['update:modelValue']);

/* endregion */
/* ------------------------------------------------------------------------------------------------------------------ */


const modelData = computed({
	get: () => {
		
		return props.modelValue.toDate();
	},
	
	set: (value) => {
		emits('update:modelValue', dayjs(value));
	}
});


</script>

<style lang="scss">

// General
$dp__font_family                  : "Inter", sans-serif !default; // Font size for the menu
$dp__border_radius                : 0.5rem !default; // Border radius everywhere
$dp__cell_border_radius           : $dp__border_radius !default; // Specific border radius for the calendar cell

// Transitions
$dp__transition_length            : 22px !default; // Passed to the translateX in animation
$dp__transition_duration          : 0.1s !default; // Transition duration

// Sizing
$dp__button_height                : 3rem !default; // size for buttons in overlays
$dp__month_year_row_height        : 35px !default; // height of the month-year select row
$dp__month_year_row_button_size   : 25px !default; // Specific height for the next/previous buttons
$dp__button_icon_height           : 20px !default; // icon sizing in buttons
$dp__cell_size                    : 35px !default; // width and height of calendar cell
$dp__cell_padding                 : 5px !default; // padding in the cell
$dp__common_padding               : 10px !default;
$dp__input_padding                : 6px 12px !default; // padding in the input
$dp__input_icon_padding           : 35px !default; // Padding on the left side of the input if icon is present
$dp__menu_min_width               : 260px !default; // Adjust the min width of the menu
$dp__action_buttons_padding       : 2px 5px !default; // Adjust padding for the action buttons in action row
$dp__row_margin                   : 5px 0 !default; // Adjust the spacing between rows in the calendar
$dp__calendar_header_cell_padding : 0.5rem !default; // Adjust padding in calendar header cells
$dp__two_calendars_spacing        : 10px !default; // Space between two calendars if using two calendars
$dp__overlay_col_padding          : 3px !default; // Padding in the overlay column
$dp__time_inc_dec_button_size     : 32px !default; // Sizing for arrow buttons in the time picker

// Font sizes
$dp__font_size                    : 15px !default; // overall font-size
$dp__preview_font_size            : 0.8rem !default; // font size of the date preview in the action row
$dp__time_font_size               : 2rem !default; // font size in the time picker


@import "@vuepic/vue-datepicker/src/VueDatePicker/style/main.scss";

.dp__theme_dark {
	--dp-background-color       : #434343;
	--dp-text-color             : #ffffff;
	--dp-hover-color            : #484848;
	--dp-hover-text-color       : #ffffff;
	--dp-hover-icon-color       : #959595;
	--dp-primary-color          : #00c64c;
	--dp-primary-text-color     : #ffffff;
	--dp-secondary-color        : #a9a9a9;
	--dp-border-color           : #141414;
	--dp-menu-border-color      : #2d2d2d;
	--dp-border-color-hover     : rgba(0, 198, 76, 0.5);
	--dp-disabled-color         : #737373;
	--dp-scroll-bar-background  : #212121;
	--dp-scroll-bar-color       : #484848;
	--dp-success-color          : #00701a;
	--dp-success-color-disabled : #428f59;
	--dp-icon-color             : #959595;
	--dp-danger-color           : #e53935;
	--dp-highlight-color        : rgba(0, 92, 178, 0.2);
}

.dp__input {
	@apply pr-4 pl-10 h-[3rem];
}

</style>