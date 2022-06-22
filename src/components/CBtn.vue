<template>
    <button 
        class="btn"
        v-bind:style="{ backgroundColor: color }"
        @click="$emit('click', $emit)"
    >
        <slot />
    </button>
</template>

<script>
export default {
    name: 'CBtn',
    props: {
        color: {
            type: String,
            default: 'teal'
        }
    }
}
</script>

<style scoped>
    .btn {
        text-decoration: none;
        border: none;
        border-radius: 4px;
        color: #fff;
        padding: 8px 16px;
        background: teal;
        opacity: 1;
        cursor: pointer;
    }

    .btn:hover {
        opacity: 0.7;
    }
</style>