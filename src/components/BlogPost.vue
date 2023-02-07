<script setup>
 //defineProps(['title', 'id', 'body','colorText'])
 //const props = defineProps(['title', 'id', 'body','colorText'])
//  console.log(props.title)
// console.log(props.id)
// console.log(props.body)
// console.log(props.colorText)

defineProps({
    title: String,
    id : Number,
    body:{
        type: String,
        default: 'sin descripcion'
    },
    colorText: String,
 })

const eventos = defineEmits(['setFavoritoProp'])

</script>

<template>
<div class="card m-2">
    <div class="card-body">
        <h5 class="card-title"
        :class= "`text-${colorText}`">
            {{ id }} - {{title}}
        </h5>
        <p> {{body}}</p>
        <button class="btn btn-outline-primary" @click="eventos('setFavoritoProp', title)">Favorito</button>
        <!-- <button class="btn btn-outline-primary" @click="$emit('setFavoritoProp', title)">Favorito</button> -->
    </div>
</div>
</template>