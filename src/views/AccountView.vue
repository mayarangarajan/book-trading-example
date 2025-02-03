<template>
    <div class="account">
        <h1>My Account</h1>
        <div class="profile-section">
            <h2>Profile Information</h2>
            <div class="user-info">
                <p><strong>Name:</strong> {{ userInfo.name }}</p>
                <p><strong>Email:</strong> {{ userInfo.email }}</p>
            </div>
        </div>
        <div class="trades-history">
            <h2>Trade History</h2>
            <div v-for="trade in tradeHistory" :key="trade.id" class="trade-item">
                <p>{{ trade.book.title }} - {{ trade.createdAt }}</p>
                <span :class="trade.status">{{ trade.status }}</span>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import type { Trade } from '../../shared/book';

export default {
    data() {
        return {
            userInfo: {
                name: 'John Doe',
                email: 'john@example.com'
            },

        }
    },
    props: {
        tradeHistory: Array<Trade>
    }
}
</script>