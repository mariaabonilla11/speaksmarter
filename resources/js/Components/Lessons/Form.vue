<script>
export default {
    name: 'LessonForm'
}

</script>

<script setup>
import FormSection from '@/Components/FormSection.vue'
import InputError from '@/Components/InputError.vue'
import InputLabel from '@/Components/InputLabel.vue'
import PrimaryButton from '@/Components/PrimaryButton.vue'
import SecondaryButton from '@/Components/SecondaryButton.vue'
import TextInput from '@/Components/TextInput.vue'
import CollectionSelector from '../Common/CollectionSelector.vue'
import {ref} from 'vue'

defineProps({
    form: {
        type: Object,
        required: true
    },
    updating: {
        type: Boolean,
        required: false,
        default: false
    },
    categories: {
        type: Object,
        required: true
    },
    levels: {
        type: Object,
        required: true
    }
})

const categoriesSelected = ref([])
const onCategories = (_categories) => {
    categoriesSelected.value = _categories
}

defineEmits(['submit'])

</script>

<template>
    <FormSection @submitted="$emit('submit')">
        <template #title>
            {{ updating ? 'Update Lesson' : 'Create new Lesson' }}
        </template>

        <template #description>
            {{ updating ? 'Update the selected lesson' : 'Create new Lesson' }}
        </template>

        <template #form>
            <div class="col-span-6 sm:col-span-6">
                <!-- INPUT NAME -->
                <InputLabel for="name" value="name"/>
                <TextInput class="mt-1 block w-full"
                id="name" v-model="form.name" type="text" autocomplete="name"/>
                <InputError :message="$page.props.errors.name" class="mt-2"/>
                
                <!-- DESCRIPTION NAME -->
                <InputLabel for="description" value="Description"/>
                <TextInput class="mt-1 block w-full"
                id="description" v-model="form.description" type="text" autocomplete="description"/>
                <InputError :message="$page.props.errors.description" class="mt-2"/>
                <br />

                <!-- FILE CONTENT URI -->
                <InputLabel for="content_uri" value="Content URI"/>
                <TextInput class="mt-1 block w-full"
                id="content_uri" v-model="form.content_uri" type="text" autocomplete="content_uri"/>
                <InputError :message="$page.props.errors.content_uri" class="mt-2"/>
                <br />

                <!-- BOTON SUBIR PDF -->
                <InputLabel value="PDF"/>
                <SecondaryButton class="mt-2 mr-2" type="button">Upload PDF</SecondaryButton>
                <InputError :message="$page.props.errors.pdf_uri" class="mt-2"/>
                <br />

                <div class="w-full mt-5">
                    <div class="flex">
                        <div class="w-1/2 mr-1">
                            <!-- LEVEL ID SELECT -->
                            <InputLabel for="level_id" value="Level"/>
                            <select id="level_id" name="level_id" class="w-full border-gray-300 focus:border-indigo-500 focus:ring-indigo-500 rounded-md shadow-sm">
                                <option v-for="level in levels" :value="level.id">{{ level.name }}</option>
                            </select>
                            <InputError :message="$page.props.errors.level_id" class="mt-2"/>
                            <br />
                        </div>

                        <div class="w-1/2 ml-1">
                            <InputLabel for="categories" value="Categories"/>
                            <CollectionSelector name="categories" id="categories" :collection="categories" @onCategories="onCategories"></CollectionSelector>
                        </div>d

                    </div>
                </div>
            </div>
        </template>


        <template #actions>
            <PrimaryButton>
                {{ updating ? 'Update' : 'Create'}}
            </PrimaryButton>
        </template>
    </FormSection>
</template>