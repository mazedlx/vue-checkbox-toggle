<template>
    <div
        class="checkbox-toggle"
        role="checkbox"
        @keydown="toggle"
        @click.stop="toggle"
        tabindex="0"
        :aria-checked="toggled"
    >
        <div
            class="checkbox-slide"
            :class="classes"
        >
            <div
                class="checkbox-switch"
                :class="classes"
            ></div>
        </div>
        <div
            v-show="showLabels"
            class="checkbox-label"
            v-html="label"
        ></div>
   </div>
</template>
<script>
export default {
    computed: {
        classes: function() {
            return {
                checked: this.toggled,
                unchecked: !this.toggled,
                disabled: this.disabled
            };
        },

        label: function() {
            return this.toggled && this.showLabels
                ? this.labelChecked
                : this.labelUnchecked;
        }
    },

    data() {
        return {
            toggled: this.value
        };
    },

    methods: {
        toggle: function(e) {
            if (this.disabled || e.keyCode === 9) { // not if disabled or tab is pressed
                e.stop();
            }
            this.toggled = ! this.toggled;
            this.$emit("input", this.toggled);
        }
    },

    props: {
        disabled: {
            type: Boolean,
            default: false
        },

        value: {
            type: Boolean,
            default: ""
        },

        showLabels: {
            type: Boolean,
            default: false
        },

        labelChecked: {
            type: String,
            default: ""
        },

        labelUnchecked: {
            type: String,
            default: ""
        },
    },
}
</script>

<style lang="sass" scoped>
    $slideWidth: 4em
    $borderRadius: 0.25em

    $switchWidth: $slideWidth/2
    $switchHeight: $slideWidth/2

    $distance: $slideWidth/2

    $switchColor: rgb(56, 74, 93)
    $sliderColorActive: rgb(103, 175, 127)
    $sliderColorInactive: rgb(211, 211, 211)

    $transitionTime: 350ms

    .checkbox-toggle
        width: $slideWidth * 3
        display: flex
        flex-direction: row
        justify-content: flex-start
        align-items: center
        margin: 0.5em

    .checkbox-slide
        width: $slideWidth
        padding: 0
        margin: 0
        border-radius: .25em
        cursor: pointer

    .checkbox-switch
        padding: 0
        margin: 0
        width: $switchWidth
        height: $switchHeight
        border-radius: $borderRadius
        background: $switchColor
        cursor: pointer

    .checkbox-label
        margin-left: 0.5em

    .checkbox-switch.checked
        transform: translateX($distance)
        transition: all $transitionTime

    .checkbox-switch.unchecked
        transition: all $transitionTime

    .checkbox-slide.checked
        transition: all $transitionTime
        background: $sliderColorActive

    .checkbox-slide.unchecked
        transition: all $transitionTime
        background: $sliderColorInactive

    .checkbox-switch.disabled
        cursor: not-allowed
        background: lighten($switchColor, 35%)

    .checkbox-slide.disabled
        cursor: not-allowd
        background: lighten($sliderColorInactive, 5%)
</style>
