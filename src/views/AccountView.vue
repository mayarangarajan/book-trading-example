<template>
    <div class="account-container">
        <h1>Your Trade History</h1>
        <div v-if="tradeHistory.length > 0">
            <div v-for="trade in tradeHistory" :key="trade.id" class="trade-item">
                <BookView :book="trade.book" />
                <p>Traded with: {{ trade.offeredBy }}</p>
                <p>Date: {{ new Date(trade.createdAt).toLocaleDateString() }}</p>
            </div>
        </div>
        <p v-else>No trades completed yet.</p>
    </div>
</template>

<script lang="ts">
import BookView from '@/components/BookView.vue';
import type { Trade } from '../../shared/book';

export default {
    components: {
        BookView
    },
    props: {
        tradeHistory: Array as () => Trade[],
    }
}
</script>

<style scoped>
.account-container {
    padding: 1rem;
}

.trade-item {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    padding: 1rem;
    border-bottom: 1px solid #ddd;
}
</style>
