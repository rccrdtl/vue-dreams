<template>
    <div>
        <Dreams subtitle="A Vue app to manage your dreams!" />

        <div class="mt-3 mb-8 md:mx-auto px-8 md:px-0 md:max-w-xl text-xs text-gray-400">
            <span v-if="! findOutMore" @click="findOutMore = ! findOutMore" class="font-semibold text-indigo-500 hover:underline cursor-pointer">Find out more</span>
            <span v-else class="font-semibold">About Vue Dreams</span>
            <div v-if="findOutMore" class="mt-2">
                <p class="mb-2">Built with Vue 3 and Tailwind CSS. Source Code available at <a href="https://github.com/riccitalia/vue-dreams" target="_blank" class="font-semibold text-indigo-500 hover:underline cursor-pointer">Github</a>.</p>
            </div>
        </div>
    </div>
</template>

<script>
    import Dreams from './components/Dreams.vue'

    export default {
        name: 'App',
        components: {
            Dreams
        },
        data: function () {
            return {
                findOutMore: false,
            }
        }
    }
</script>

<style scoped>
</style>
