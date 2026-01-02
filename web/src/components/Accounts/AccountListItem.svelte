<script lang="ts">
    import { accounts, activeAccount, popupDetails, atm, translations } from "../../store/stores";
    import { formatMoney } from "../../utils/misc";
    export let account:any;

    function handleAccountClick(id: any) {
        activeAccount.update(() => id);
    };

    let isAtm: boolean;
    function handleButton(id:string, type:string) {
        let account = $accounts.find((accountItem: any) => id === accountItem.id);
        popupDetails.update(() => ({ actionType: type, account }));
    }

    atm.subscribe((usingAtm: boolean) => {
        isAtm = usingAtm;
    });
</script>

<div class="account-card" on:click={()=>handleAccountClick(account.id)} on:keydown={()=>{}}>
    <div class="card-content">
        <div class="card-top">
            <div class="card-info">
                <h4>{account.type}{$translations.account}</h4>
                <p class="account-id">{account.id}</p>
                <p class="account-name">{account.name}</p>
            </div>
            <div class="card-icons">
                <i class="fas fa-credit-card"></i>
                <i class="fas fa-credit-card"></i>
            </div>
        </div>
        <div class="card-amount">
            <strong>{formatMoney(account.amount)}</strong>
        </div>
    </div>
</div>

<style>
    .account-card {
        min-width: 280px;
        background: linear-gradient(135deg, #1e3a5f 0%, #2a4a7f 100%);
        padding: 1.5rem;
        border-radius: 12px;
        cursor: pointer;
        border: 2px solid rgba(0, 149, 255, 0.3);
        transition: all 0.3s ease;
        color: white;
    }

    .account-card:hover {
        border-color: var(--clr-blue);
        box-shadow: 0 0 20px rgba(0, 149, 255, 0.4);
    }

    .card-content {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 100%;
    }

    .card-top {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
    }

    .card-info h4 {
        font-size: 0.95rem;
        margin-bottom: 0.5rem;
        color: rgba(255, 255, 255, 0.8);
    }

    .account-id {
        font-size: 0.85rem;
        color: rgba(255, 255, 255, 0.6);
        margin-bottom: 0.3rem;
    }

    .account-name {
        font-size: 0.9rem;
        color: rgba(255, 255, 255, 0.7);
    }

    .card-icons {
        display: flex;
        gap: 0.5rem;
        opacity: 0.5;
    }

    .card-icons i {
        font-size: 1.2rem;
    }

    .card-amount {
        text-align: right;
    }

    .card-amount strong {
        font-size: 1.3rem;
        color: var(--clr-blue);
    }
</style>
