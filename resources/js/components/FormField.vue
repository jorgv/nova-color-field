<template>
    <default-field :field="field">
        <template slot="field">
            <div class="inline-flex mb-2">
                <div class="color-input rounded-l-lg border-r-0 h-100 border border-60 color-input-value" v-bind:style="{ backgroundColor: value, width: '36px' }"></div>
                <input :id="field.name" type="text"
                       class="w-25 form-control form-input form-input-bordered color-input rounded-l-none"
                       :class="errorClasses"
                       :placeholder="field.name"
                       v-model="value"
                />
            </div>
            <slider-picker :id="field.name" :class="errorClasses" :value="value" @input="handleChange"></slider-picker>
            <p v-if="hasError" class="my-2 text-danger">
                {{ firstError }}
            </p>
        </template>
    </default-field>
</template>

<script>
    import {FormField, HandlesValidationErrors} from 'laravel-nova'

    export default {
        mixins: [FormField, HandlesValidationErrors],

        props: ['resourceName', 'resourceId', 'field'],

        methods: {
            /*
             * Set the initial, internal value for the field.
             */
            setInitialValue() {
                this.value = this.field.value || ''
            },

            /**
             * Fill the given FormData object with the field's internal value.
             */
            fill(formData) {
                formData.append(this.field.attribute, this.value || '')
            },

            /**
             * Update the field's internal value.
             */
            handleChange(value) {
                this.value = value.hex;
            }
        }
    }
</script>
