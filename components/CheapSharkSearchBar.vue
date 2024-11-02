<template>
    <div class="text mx-auto mb-32 flex max-w-screen-sm items-center justify-center">
        <div
            class="p-1.5 rounded-full bg-gradient-to-r from-[#180161] via-[#4F1787] to-[#EB3678] hover:via-[#EB3678] hover:to-[#FB773C] has-[:focus]:to-[#FB773C] has-[:focus]:via-[#EB3678]">
            <div class="flex rounded-full overflow-hidden max-w-md mx-auto font-[sans-serif]">
                <input type="text" v-model="search" @input="onChange" placeholder="Search Game..."
                    @keydown.down="onArrowDown" @keydown.up="onArrowUp" @keydown.enter="onEnter"
                    class="rounded-full w-full outline-none bg-white text-gray-600 text-base px-4 py-3" />
                <ul v-show="isOpen" class="autocomplete-results">
                    <li v-if="isLoading" class="loading">Loading results...</li>
                    <li v-else v-for="(result, i) in results" :key="i" @click="setResult(result)"
                        class="autocomplete-result" :class="{ 'is-active': i === arrowCounter }">
                        {{ result }}
                    </li>
                </ul>
                <button type='button' class="flex items-center justify-center bg-transparent px-4">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 192.904 192.904" width="24px"
                        class="fill-white">
                        <path
                            d="m190.707 180.101-47.078-47.077c11.702-14.072 18.752-32.142 18.752-51.831C162.381 36.423 125.959 0 81.191 0 36.422 0 0 36.423 0 81.193c0 44.767 36.422 81.187 81.191 81.187 19.688 0 37.759-7.049 51.831-18.751l47.079 47.078a7.474 7.474 0 0 0 5.303 2.197 7.498 7.498 0 0 0 5.303-12.803zM15 81.193C15 44.694 44.693 15 81.191 15c36.497 0 66.189 29.694 66.189 66.193 0 36.496-29.692 66.187-66.189 66.187C44.693 147.38 15 117.689 15 81.193z">
                        </path>
                    </svg>
                </button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'SearchAutocomplete',
    props: {
        items: {
            type: Array,
            required: false,
            default: () => [],
        },
        isAsync: {
            type: Boolean,
            required: false,
            default: false,
        },
    },
    data() {
        return {
            isOpen: false,
            results: [],
            search: '',
            isLoading: false,
            arrowCounter: -1,
        };
    },
    watch: {
        items: function (value, oldValue) {
            if (value.length !== oldValue.length) {
                this.results = value;
                this.isLoading = false;
            }
        },
    },
    mounted() {
        document.addEventListener('click', this.handleClickOutside)
    },
    destroyed() {
        document.removeEventListener('click', this.handleClickOutside)
    },
    methods: {
        setResult(result) {
            this.search = result;
            this.isOpen = false;
            this.$emit('selected', result)
        },
        filterResults() {
            this.results = this.items.filter((item) => {
                return item.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
            });
        },
        onChange() {
            this.$emit('input', this.search);

            if (this.isAsync) {
                this.isLoading = true;
            } else {
                this.filterResults();
                this.isOpen = true;
            }
        },
        handleClickOutside(event) {
            if (!this.$el.contains(event.target)) {
                this.isOpen = false;
                this.arrowCounter = -1;
            }
        },
        onArrowDown() {
            if (this.arrowCounter < this.results.length - 1) {
                this.arrowCounter = this.arrowCounter + 1;
            } else {
                this.arrowCounter = 0;
            }
        },
        onArrowUp() {
            if (this.arrowCounter > 0) {
                this.arrowCounter = this.arrowCounter - 1;
            } else {
                this.arrowCounter = this.results.length - 1;
            }
        },
        onEnter() {
            this.search = this.results[this.arrowCounter];
            this.isOpen = false;
            this.arrowCounter = -1;
        },
    },
};
</script>
<style>
@keyframes appearing {
    0% {
        opacity: 0%;
    }

    100% {
        opacity: 100%;
    }
}

.text {
    animation-duration: 1.5s;
    animation-name: appearing;
    animation-iteration-count: 1;
}

.autocomplete-results {
    padding: 5px;
    margin: 47px 0 0 10px;
    width: 220px;
    height: auto;
    border-radius: 8px;
    max-height: 6em;
    overflow: auto;
    position: absolute;
    background-image: linear-gradient(to bottom right, #180161, #4F1787, #EB3678);
    color: white;
    border: 0 solid #FB773C;
    border-width: 0 0 1px 0;
}

.autocomplete-result {
    font-size: 1.1rem;
    font-weight: 500;
    list-style: none;
    text-align: left;
    cursor: pointer;
    padding: 0 5px;
    border: 0 solid #FB773C;
    border-width: 1px 0 0 0;
}

.autocomplete-result.is-active,
.autocomplete-result:hover {
    background-color: #FB773C;
}
</style>