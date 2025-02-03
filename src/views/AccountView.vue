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
                <p>{{ trade.book }} - {{ trade.date }}</p>
                <span :class="trade.status">{{ trade.status }}</span>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
export default {
    data() {
        return {
            userInfo: {
                name: 'John Doe',
                email: 'john@example.com'
            },
            tradeHistory: [
                {
                    id: 1,
                    book: 'The Great Gatsby',
                    cover: 'https://i0.wp.com/americanwritersmuseum.org/wp-content/uploads/2018/02/CK-3.jpg?resize=267%2C400&ssl=1',
                    date: '2025-01-10',
                    status: 'completed'
                }
            ]
        }
    }
}
</script>