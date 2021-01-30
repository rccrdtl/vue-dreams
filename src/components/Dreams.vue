<template>
    <div class="md:mt-16 md:mx-auto md:max-w-xl md:border md:border-gray-200 md:rounded-md md:shadow-sm">
        <div class="py-4 px-4 md:px-0 border-b text-center bg-gray-50 md:rounded-t-md">
            <h1 class="text-xl text-pink-500 font-bold">Vue Dreams</h1>
            <p>{{ subtitle }} <span class="tracking-widest">😊💭✨</span></p>
        </div>
        <div class="px-8 pt-6 mb:pt-8 pb-4 border-b border-gray-200">
            <ol v-if="dreams.length > 0" class="mt-2 ml-12 list-decimal">
                <li v-for="dream in dreams" :key="dream.id" class="mb-4 pl-1">
                    <span :class="{ 'line-through': dream.done }">{{ dream.content }}</span>
                    <div class="mt-1 text-xs">
                        <span v-if="! dream.done" @click="toggleDone(dream.id)" class="mr-4 font-semibold text-indigo-500 hover:underline cursor-pointer">Completed</span>
                        <span @click="removeDream(dream.id)" class="font-semibold text-indigo-500 hover:underline cursor-pointer">Delete</span>
                    </div>
                </li>
            </ol>
            <p v-else class="mt-2 mb-4 md:mb-3">Oh no! There are no dreams yet! 🥺</p>
        </div>
        <div class="px-8 pt-6 mb:pt-8 pb-8 border-b border-gray-200">
            <p class="mb-4 font-bold">Add a new dream:</p>
            <p v-if="errorMessage !== ''" class="mb-2 font-bold text-red-500">{{ errorMessage }}</p>
            <form @submit.prevent="addDream">
                <input v-model="newDream" type="text" placeholder="Dream big" class="mr-2 py-2 px-3 border rounded">
                <input type="submit" value="Add" class="py-2 px-3 font-semibold text-white bg-green-400 rounded cursor-pointer">
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Dreams',
        props: {
            subtitle: String
        },
        data: function () {
            return {
                dreams: [
                    { id: 0, content: 'Become a good chef', done: false },
                    { id: 1, content: 'Open a cozy little coffee shop', done: false },
                    { id: 2, content: 'Learn Italian', done: false }
                ],
                newDream: '',
                errorMessage: ''
            }
        },
        mounted: function () {
            this.sortDreams();
        },
        methods: {
            addDream: function () {
                let newDream = this.newDream.trim();

                if (newDream === '') {
                    this.errorMessage = 'You cannot dream of nothing!';

                    return;
                }

                this.dreams.push({ id: this.dreams.length, content: this.newDream, done: false });
                this.sortDreams();
                this.newDream = '';
                this.errorMessage = '';
            },
            toggleDone: function (id) {
                this.dreams = this.dreams.map((dream) => {
                    if (dream.id === id) {
                        return { id: dream.id, content: dream.content, done: true };
                    } else {
                        return dream;
                    }
                });

                this.sortDreams();
            },
            sortDreams: function () {
                this.dreams.sort((a, b) => (a.done > b.done) ? 1 : (a.done === b.done) ? ((a.content.toLowerCase() > b.content.toLowerCase()) ? 1 : -1) : -1);
            },
            removeDream: function (id) {
                this.dreams = this.dreams.filter((dream) => dream.id !== id);
            }
        },
        computed: {
            openDreams: function () {
                return this.dreams.filter((dream) => dream.done === false );
            },
            closedDreams: function () {
                return this.dreams.filter((dream) => dream.done === true );
            }
        }
    }
</script>

<style scoped>
</style>
