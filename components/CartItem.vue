<template>
  <div class="flex justify-start my-2">
    
  </div>
</template>

<script lang="ts" setup>
    import { useUserStore } from "~/stores/user"

    const userStore = useUserStore()

    const props = defineProps(['product', 'selectedArray'])
    const { product, selectedArray } = toRefs(props)

    const emit = defineEmits(['selectedRadio'])

    let isHover = ref(false)
    let isSelected = ref(false)


    const removeFromCart = () => {
        userStore.cart.forEach((prod, index) => {
            if (prod.id === product.value.id) {
                userStore.cart.splice(index, 1)
            }
        })
    }

    watch(() => isSelected.value, (val) => {
        emit('selectedRadio', { id: product.value.id, val: val })
    })
</script>
