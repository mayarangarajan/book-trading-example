<template>
    <div class="search">
        <h1>Search Books</h1>
        <div class="search-controls">
            <input v-model="searchQuery" placeholder="Enter title or author..." @input="performSearch">
            <select v-model="searchType">
                <option value="title">Title</option>
                <option value="author">Author</option>
            </select>
        </div>
        <div class="search-results">
            <div v-for="book in searchResults" :key="book.id" class="book-item">
                <h3>{{ book.title }}</h3>
                <p>{{ book.author }}</p>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import type { Book } from '../../shared/book'

export default {
    data() {
        return {
            searchQuery: '',
            searchType: 'title' as 'title' | 'author',
            searchResults: [] as Book[]
        }
    },
    methods: {
        performSearch(): void {
            try {
                // this is just to test that the search works
                const data: Book[] = [
                    {
                        id: 1,
                        title: 'The Great Gatsby',
                        author: 'F. Scott Fitzgerald',
                        cover: 'https://i0.wp.com/americanwritersmuseum.org/wp-content/uploads/2018/02/CK-3.jpg?resize=267%2C400&ssl=1'
                    },
                    {
                        id: 2,
                        title: '1984',
                        author: 'George Orwell',
                        cover: 'https://m.media-amazon.com/images/I/61NAx5pd6XL.jpg'
                    }
                ] as Book[]
                // const response = await fetch(
                //     `/api/books/search?q=${this.searchQuery}&type=${this.searchType}`
                // )
                // const data = await response.json()
                this.searchResults = data as Book[]
            } catch (error) {
                console.error('Error performing search:', error)
                this.searchResults = []
            }
        }
    }
}
</script>