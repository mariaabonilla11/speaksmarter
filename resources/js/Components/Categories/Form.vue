<script>
export default {
    name: 'CategoryForm'
}

</script>

<script setup>
import FormSection from '@/Components/FormSection.vue'
import InputError from '@/Components/InputError.vue'
import InputLabel from '@/Components/InputLabel.vue'
import PrimaryButton from '@/Components/PrimaryButton.vue'
import TextInput from '@/Components/TextInput.vue'


defineProps({
    form: {
        type: Object,
        required: true
    },
    updating: {
        type: Boolean,
        required: false,
        default: false
    }
})
defineEmits(['submit'])

</script>

<template>
    <FormSection @submitted="$emit('submit')">
        <template #title>
            {{ updating ? 'Update Category' : 'Create new Category' }}
        </template>

        <template #description>
            {{ updating ? 'Update the selected category' : 'Create new Category' }}
        </template>

        <template #form>
            <div class="col-span-6 sm:col-span-6">
                <InputLabel for="name" value="name"/>
                <TextInput class="mt-1 block w-full"
                id="name" v-model="form.name" type="text" autocomplete="name"/>
                <InputError :message="$page.props.errors.name" class="mt-2"/>
            </div>
        </template>


        <template #actions>
            <PrimaryButton>
                {{ updating ? 'Update' : 'Create'}}
            </PrimaryButton>
        </template>
    </FormSection>
</template>