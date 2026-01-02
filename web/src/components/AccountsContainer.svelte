<script lang="ts">
    import AccountsList from "./Accounts/AccountsList.svelte";
    import AccountTransactionsList from "./Accounts/AccountTransactionsList.svelte";
    import { accounts } from '../store/stores';
    import { formatMoney } from "../utils/misc";
</script>

<div class="container">
    <div class="sidebar">
        <div class="logo">
            <i class="fas fa-layer-group"></i>
        </div>
        <nav class="nav-menu">
            <div class="nav-item active">
                <i class="fas fa-th"></i>
                <span>Dashboard</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-wallet"></i>
                <span>Accounts</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-exchange-alt"></i>
                <span>Transfer</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-history"></i>
                <span>Transactions</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-file-invoice"></i>
                <span>Invoices</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-plus-circle"></i>
                <span>Deposit</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-minus-circle"></i>
                <span>Withdraw</span>
            </div>
        </nav>
    </div>

    <div class="main-content">
        <div class="header">
            <h1>Dashboard</h1>
            <div class="search-bar">
                <input type="text" placeholder="Search...">
            </div>
        </div>

        <div class="accounts-section">
            <AccountsList />
        </div>

        <div class="content-grid">
            <div class="card weekly-summary">
                <h3>Weekly summary</h3>
                <div class="summary-item">
                    <span>Income</span>
                    <span class="amount">$0</span>
                </div>
                <div class="summary-item">
                    <span>Expenses</span>
                    <span class="amount negative">$0</span>
                </div>
                <div class="summary-item">
                    <span>Report</span>
                </div>
            </div>

            <div class="card transactions-card">
                <div class="card-header">
                    <h3>Latest transactions</h3>
                    <span class="badge">3</span>
                </div>
                <AccountTransactionsList />
                <div class="view-all">VIEW ALL</div>
            </div>

            <div class="card invoices-card">
                <div class="card-header">
                    <h3>Unpaid invoices</h3>
                    <span class="badge">0</span>
                </div>
                <div class="view-all">VIEW ALL</div>
            </div>
        </div>

        <div class="wallet-info">
            <i class="fa-solid fa-wallet fa-fw"></i>
            {#if $accounts && $accounts.length > 0}
                {formatMoney($accounts[0].cash)}
            {:else}
                $0
            {/if}
        </div>
    </div>
</div>

<style>
    .container {
        display: flex;
        width: 100%;
        height: 100vh;
        background-color: var(--clr-primary-dark);
        color: white;
    }

    .sidebar {
        width: 120px;
        background-color: #0f1419;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2rem 1rem;
        gap: 2rem;
    }

    .logo {
        font-size: 2rem;
        color: var(--clr-blue);
        cursor: pointer;
    }

    .nav-menu {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        flex: 1;
    }

    .nav-item {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 0.5rem;
        cursor: pointer;
        color: #888;
        font-size: 0.8rem;
        transition: all 0.3s ease;
    }

    .nav-item i {
        font-size: 1.5rem;
    }

    .nav-item.active {
        color: var(--clr-blue);
    }

    .nav-item:hover {
        color: var(--clr-blue);
    }

    .main-content {
        flex: 1;
        padding: 2rem;
        overflow-y: auto;
    }

    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 2rem;
    }

    .header h1 {
        font-size: 2rem;
    }

    .search-bar {
        width: 300px;
    }

    .search-bar input {
        width: 100%;
        padding: 0.8rem 1rem;
        background-color: rgba(255, 255, 255, 0.1);
        border: 1px solid rgba(255, 255, 255, 0.2);
        border-radius: 5px;
        color: white;
    }

    .accounts-section {
        margin-bottom: 2rem;
    }

    .content-grid {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 1.5rem;
        margin-bottom: 2rem;
    }

    .card {
        background: linear-gradient(135deg, #1e3a5f 0%, #2a4a7f 100%);
        border-radius: 8px;
        padding: 1.5rem;
        border: 1px solid rgba(0, 149, 255, 0.2);
    }

    .card h3 {
        color: var(--clr-blue);
        margin-bottom: 1rem;
        font-size: 1rem;
    }

    .card-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 1rem;
    }

    .badge {
        background-color: var(--clr-blue);
        color: white;
        padding: 0.25rem 0.75rem;
        border-radius: 20px;
        font-size: 0.8rem;
        font-weight: bold;
    }

    .summary-item {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
        font-size: 0.9rem;
    }

    .amount {
        color: var(--clr-blue);
        font-weight: bold;
    }

    .amount.negative {
        color: #ff6b6b;
    }

    .view-all {
        text-align: center;
        color: var(--clr-blue);
        cursor: pointer;
        margin-top: 1rem;
        font-size: 0.85rem;
        text-transform: uppercase;
        letter-spacing: 1px;
    }

    .view-all:hover {
        text-decoration: underline;
    }

    .wallet-info {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        font-size: 1.2rem;
        color: var(--clr-blue);
    }
</style>
