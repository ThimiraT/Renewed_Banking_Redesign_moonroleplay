<script lang="ts">
    import { accounts, translations } from "../../store/stores";
    import AccountListItem from "./AccountListItem.svelte";
</script>

<div class="accounts-container">
    <div class="accounts-grid">
        {#each $accounts as account (account.id)}
            <AccountListItem {account} />
        {/each}
        <div class="add-account">
            <i class="fas fa-plus"></i>
        </div>
    </div>
</div>

<style>
    .accounts-container {
        width: 100%;
    }

    .accounts-grid {
        display: flex;
        gap: 1.5rem;
        overflow-x: auto;
        padding-bottom: 1rem;
    }

    .add-account {
        min-width: 200px;
        height: 120px;
        background: transparent;
        border: 2px dashed rgba(0, 149, 255, 0.5);
        border-radius: 8px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        font-size: 2rem;
        color: rgba(0, 149, 255, 0.5);
        transition: all 0.3s ease;
    }

    .add-account:hover {
        border-color: var(--clr-blue);
        color: var(--clr-blue);
        background: rgba(0, 149, 255, 0.1);
    }
</style>
