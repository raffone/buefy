<template>
    <div class="control" :class="{ 'is-expanded': expanded }">
        <label
            class="b-checkbox checkbox button"
            ref="label"
            :class="[checked ? type : null, size, {
                'is-disabled': disabled,
                'is-focused': isFocused
            }]"
            :disabled="disabled"
            @click="focus"
            @keydown.prevent.enter="$refs.label.click()">
            <slot/>
            <input
                v-model="computedValue"
                type="checkbox"
                ref="input"
                @click.stop
                :disabled="disabled"
                :required="required"
                :name="name"
                :value="nativeValue"
                @focus="isFocused = true"
                @blur="isFocused = false"
                :autocomplete="autocomplete"
                :true-value="trueValue"
                :false-value="falseValue"
                :aria-labelledby="ariaLabelled"
                :indeterminate.prop="indeterminate"
                >
        </label>
    </div>
</template>

<script>
import CheckRadioMixin from '../../utils/CheckRadioMixin.js'

export default {
    name: 'BCheckboxButton',
    mixins: [CheckRadioMixin],
    props: {
        type: {
            type: String,
            default: 'is-primary'
        },
        expanded: Boolean,
        indeterminate: Boolean,
        ariaLabelledby: String,
        trueValue: {
            type: [String, Number, Boolean, Function, Object, Array],
            default: true
        },
        falseValue: {
            type: [String, Number, Boolean, Function, Object, Array],
            default: false
        },
        autocomplete: {
            type: String,
            default: 'on'
        }
    },
    data() {
        return {
            isFocused: false
        }
    },
    computed: {
        checked() {
            if (Array.isArray(this.newValue)) {
                return this.newValue.indexOf(this.nativeValue) >= 0
            }
            return this.newValue === this.nativeValue
        }
    }
}
</script>
