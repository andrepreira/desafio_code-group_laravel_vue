<script>
    import { range } from 'lodash'
    export default {
        props: ['source'],
        data() {
            return {
                    pages: []
            }
        },
        methods: {
            navigate (ev, page) {
                ev.preventDefault()
                this.$emit('navigate', page)
            },
            nextPrev (ev, page) {
                if (page == 0 || page == this.source.last_page+1) {
                    return;
                }
               this.navigate(ev, page)
            }
        },
        watch: {
            source () {
                this.pages = range(1, this.source.last_page+1)
            }
        }
    }
</script>

<template>
    <nav>
        <ul class="pagination">
            <li class="page-item" :class="{disabled: source.current_page == 1}">
                <a class="page-link" href="#" @click="nextPrev($event, source.current_page-1)" aria-label="Previous">
                    <span aria-hidden="true">&laquo;</span>
                </a>
            </li>
             <li class="page-item" :class="{active: source.current_page == page}" v-for="page in pages" :key="page">
                <a class="page-link" href="#" @click="navigate($event, page)">{{  page }}</a>
            </li>
            <li class="page-item" :class="{disabled: source.current_page == this.source.last_page}">
                <a class="page-link" href="#" @click="nextPrev($event, source.current_page+1)" aria-label="Next">
                    <span aria-hidden="true">&raquo;</span>
                </a>
            </li>
        </ul>
    </nav>
</template>
