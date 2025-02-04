<template>
    <div class="trades-container">
        <div class="trades-section">
            <h1>Incoming Trades</h1>
            <div v-for="trade in incomingTrades" :key="trade.id" class="trade-card">
                <BookView :book="trade.book" />
                <div class="trade-details">
                    <p>Offered by: {{ trade.offeredBy }}</p>
                    <p>Status: {{ trade.status }}</p>
                </div>
                <div class="trade-actions">
                    <button class="accept-btn" @click="acceptTrade(trade)">Accept</button>
                    <button class="decline-btn" @click="declineTrade(trade.id)">Decline</button>
                </div>
            </div>
        </div>
        <div class="trades-section">
            <h1>Your Pending Trade Requests</h1>
            <div class="trades-list">
                <div v-for="trade in outgoingTrades" :key="trade.id" class="trade-card">
                    <BookView :book="trade.book" />
                    <div class="trade-details">
                        <p>Sending to: {{ trade.offeredTo }}</p>
                        <p>Status: {{ trade.status }}</p>
                    </div>
                    <div class="trade-actions" v-if="trade.status === 'pending'">
                        <button @click="cancelTrade(trade.id)" class="cancel-btn">Cancel Request</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import BookView from '@/components/BookView.vue';
import type { Trade, OutgoingTrade } from '../../shared/book';

export default {
    components: {
        BookView
    },
    props: {
        incomingTrades: Array as () => Trade[],
        outgoingTrades: Array as () => OutgoingTrade[],
    },
    emits: ['tradeAccepted'],
    methods: {
        acceptTrade(trade: Trade): void {
            this.$emit('tradeAccepted', trade);

            // Remove the accepted trade from incomingTrades
            this.incomingTrades = this.incomingTrades.filter(t => t.id !== trade.id);
        },
        declineTrade(tradeId: number): void {
            this.incomingTrades = this.incomingTrades.filter(t => t.id !== tradeId);
        },
        cancelTrade(tradeId: number): void {
            this.outgoingTrades = this.outgoingTrades.filter(t => t.id !== tradeId);
        }
    }
}
</script>

<style scoped>
.trades-container {
    display: grid;
    gap: 2rem;
    padding: 1rem;
}

.trades-section {
    padding: 1rem;
    border-radius: 8px;
}

.trades-list {
    display: grid;
    gap: 1rem;
}

.trade-card {
    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: 1rem;
    padding: 1rem;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.trade-actions {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

button {
    padding: 0.5rem 1rem;
    border-radius: 4px;
    border: none;
    cursor: pointer;
}

.accept-btn {
    background: #4CAF50;
    color: white;
}

.decline-btn {
    background: #f44336;
    color: white;
}

.cancel-btn {
    background: #aaaaaa;
    color: white;
}
</style>
