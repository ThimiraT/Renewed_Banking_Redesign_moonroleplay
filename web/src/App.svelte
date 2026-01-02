<script lang="ts">
    import VisibilityProvider from "./providers/VisibilityProvider.svelte";
    import { debugData } from "./utils/debugData";
    import AccountsContainer from "./components/AccountsContainer.svelte";
    import Popup from "./components/Popup.svelte";
    import Loading from "./components/Loading.svelte";
    import Notification from "./components/Notification.svelte";
    import { popupDetails, loading, notify } from "./store/stores";

    debugData([
        {
            action: "setVisible",
            data: {
                status: true,
                loading: false,
                atm: false,
                accounts: [
                    {
                        id: "1001",
                        type: "Checking",
                        name: "Main Account",
                        amount: 5000,
                        isFrozen: false,
                        cash: 2500,
                        transactions: [
                            {
                                trans_id: "TX001",
                                message: "Salary Deposit",
                                receiver: "Employer",
                                amount: 2000,
                                date: "2024-01-02"
                            },
                            {
                                trans_id: "TX002",
                                message: "Bill Payment",
                                receiver: "Electric Company",
                                amount: 150,
                                date: "2024-01-01"
                            }
                        ]
                    },
                    {
                        id: "1002",
                        type: "Savings",
                        name: "Savings Account",
                        amount: 10000,
                        isFrozen: false,
                        cash: 0,
                        transactions: []
                    },
                    {
                        id: "1003",
                        type: "Business",
                        name: "Business Account",
                        amount: 25000,
                        isFrozen: false,
                        cash: 0,
                        transactions: []
                    }
                ]
            },
        },
        {
            action: "updateLocale",
            data: {
                translations: {
                    accounts: "Accounts",
                    account_search: "Search accounts...",
                    account_not_found: "No accounts found",
                    transactions: "Transactions",
                    trans_search: "Search transactions...",
                    trans_not_found: "No transactions found",
                    account: "Account",
                    balance: "Balance",
                    deposit_but: "Deposit",
                    withdraw_but: "Withdraw",
                    transfer_but: "Transfer",
                    frozen: "Account Frozen",
                    bank_name: "Banking System"
                },
                currency: "USD"
            }
        }
    ], 500);
</script>
</script>

<svelte:head>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.2/css/all.min.css" integrity="sha512-1sCRPdkRXhBV2PBLUdRb4tMg1w2YPf37qatUFeS7zlBy7jJI8Lf4VHwWfZZfpXtYSLy85pkm9GaYVYMfw5BC1A==" crossorigin="anonymous" referrerpolicy="no-referrer" />
</svelte:head>
<VisibilityProvider>
    <AccountsContainer />
    {#if $popupDetails.actionType !== ""}
        <Popup />
    {/if}
    {#if $notify !== ""}
        <Notification />
    {/if}
</VisibilityProvider>
{#if $loading}
    <Loading />
{/if}
