<template>
    <form @submit.prevent="onSave">
        <div class="form_group">
            <label for="">Name:</label>
            <input v-model="editedDeck.name" class="form_control" type="text" placeholder="Please enter name deck">
        </div>
        <div class="form_group">
            <label for="">Description:</label>
            <textarea v-model="editedDeck.description" class="form_control" placeholder="Please enter description" />
        </div>
        <div class="form_group">
            <label for="">Thumbnail:</label>
            <input v-model="editedDeck.thumbnail" class="form_control" type="text" placeholder="https://example.com">
            <div class="preview"></div>
        </div>
        <div class="form_group d_flex justify_content_end">
            <button class="btn btn_danger" @click.prevent="closeModal">Close Modal</button>
            <button class="btn btn_success ml_3" type="submit" >
                {{editedDeck && editedDeck.id ? 'Edit' : 'Create'  }}
            </button>

        </div>
    </form>
</template>

<script>
export default {
    props: {
        deck: {
            type: Object,
            default: () => ({
                name: '',
                description: '',
                thumbnail: ''
            })
        }
    },
    data() {
        return {
            editedDeck: this.deck
                ? { ...this.deck }
                : {
                    name: '',
                    description: '',
                    thumbnail: ''
                }
        }
    },
    methods: {
        closeModal() {
            this.$modal.close({ name: 'DeckFormModal' })
        },
        onSave() {
            this.$emit('submit', this.editedDeck)
        }
    }
}

</script>
