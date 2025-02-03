<template>
    <div class="trades">
        <h1>Active Trades</h1>
        <div class="trades-list">
            <div v-for="trade in activeTrades" :key="trade.id" class="trade-card">
                <div class="trade-details">
                    <h3>{{ trade.book.title }}</h3>
                    <p>Offered by: {{ trade.offeredBy }}</p>
                    <p>Status: {{ trade.status }}</p>
                </div>
                <div class="trade-actions">
                    <button @click="acceptTrade(trade.id)">Accept</button>
                    <button @click="declineTrade(trade.id)">Decline</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import type { Trade } from '../../shared/book'
export default {
    data() {
        return {
            activeTrades: [] as Trade[]
        }
    },
    methods: {
        acceptTrade(tradeId: number): void {
            // Implement accept logic
        },
        declineTrade(tradeId: number): void {
            // Implement decline logic
        }
    },
    created() {
        // TODO: make a request to the server to get the active trades
        this.activeTrades = [
            {
                id: 1,
                book: {
                    cover: 'https://m.media-amazon.com/images/I/8125BDk3l9L._SL1500_.jpg',
                    id: 3,
                    title: 'The Catcher in the Rye',
                    author: 'J.D. Salinger'
                },
                offeredBy: 'Jane Smith',
                status: 'pending',
                createdAt: '2025-01-31'
            }
        ]
    }
}
</script>