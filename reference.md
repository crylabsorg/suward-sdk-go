# Reference
## Payments
<details><summary><code>client.Payments.ListPayments() -> *suwardsdkgo.CryptopayListPaymentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List payments for a project
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1PaymentsRequest{}
client.Payments.ListPayments(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order:** `*suwardsdkgo.GetV1PaymentsRequestOrder` — Sort order (asc/desc)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Limit (default 20, max 100)
    
</dd>
</dl>

<dl>
<dd>

**lastID:** `*string` — Last ID for pagination
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.CreatePayment(request) -> *suwardsdkgo.CryptopayPaymentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new payment
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.CryptopayCreatePaymentRequest{}
client.Payments.CreatePayment(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**activationFlowSeconds:** `*int` — Grace period in seconds before the payment window starts counting, giving the customer time to open the checkout before the timer runs. Optional; range 1 to 3600 (1 hour).
    
</dd>
</dl>

<dl>
<dd>

**amount:** `*string` — Merchant base amount, integer string in the asset's smallest unit. When a fee payer is customer the customer is charged more than this (gross); when merchant (default) the fee is deducted from the merchant's proceeds.
    
</dd>
</dl>

<dl>
<dd>

**asset:** `*suwardsdkgo.CryptopayAssetID` — Asset the customer will pay in, as an asset id-string (e.g. USDT_ARBITRUM). Required only when the project allows more than one asset; when the project has a single asset it may be omitted. The full set of accepted values is served live at GET /v1/assets.
    
</dd>
</dl>

<dl>
<dd>

**networkFeePayer:** `*suwardsdkgo.CryptopayFeePayer` — Who bears the network (gas) fee. Default merchant.
    
</dd>
</dl>

<dl>
<dd>

**serviceFeePayer:** `*suwardsdkgo.CryptopayFeePayer` — Who bears the platform (service) fee. Default merchant.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Your own identifier for this payment. Echoed back on the payment and its webhooks, and can be appended to the return URL as a redirect parameter. Optional.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `map[string]any` — Arbitrary JSON key/value data to attach to the payment. Stored and echoed back unchanged on the payment and its webhooks; never sent on-chain. Use it to correlate the payment with your own records.
    
</dd>
</dl>

<dl>
<dd>

**paymentWindowSeconds:** `*int` — How long the payment stays open for funding, in seconds. Optional; when omitted the project default applies. Range 300 (5 minutes) to 86400 (24 hours).
    
</dd>
</dl>

<dl>
<dd>

**redirectConfig:** `*suwardsdkgo.CryptopayRedirectConfigDto` — Optional "return to store" redirect configuration: the base URL the customer is sent back to after paying, plus which payment identifiers to append as query parameters.
    
</dd>
</dl>

<dl>
<dd>

**underpaymentTolerance:** `*string` — Amount the customer may underpay and still have the payment accepted, as an integer string in the asset's smallest unit (same scale as amount). Optional; if set it must be >= 0 and strictly less than amount. Default 0 (exact amount required). Example: for amount "10000000" (10 USDT) a value of "500000" allows a 0.50 USDT shortfall.
    
</dd>
</dl>

<dl>
<dd>

**webhookURL:** `*string` — Webhook URL to receive this payment's events. Optional; overrides the project's default webhook URL for this payment only.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.GetPayment(PaymentID) -> *suwardsdkgo.GetV1PaymentsPaymentIDResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns full payment details when called with an API key (merchant view).
Returns limited payment details when called without an API key (customer view).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1PaymentsPaymentIDRequest{
        PaymentID: "paymentId",
    }
client.Payments.GetPayment(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**paymentID:** `string` — Payment ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.ActivatePayment(PaymentID) -> *suwardsdkgo.CryptopayPublicPaymentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Activate a payment (public, customer-facing)
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.PostV1PaymentsPaymentIDActivateRequest{
        PaymentID: "paymentId",
    }
client.Payments.ActivatePayment(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**paymentID:** `string` — Payment ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.CancelPayment(PaymentID) -> *suwardsdkgo.CryptopayPaymentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a payment
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.PostV1PaymentsPaymentIDCancelRequest{
        PaymentID: "paymentId",
    }
client.Payments.CancelPayment(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**paymentID:** `string` — Payment ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.SimulatePayment(PaymentID, request) -> *suwardsdkgo.CryptopayPaymentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Simulate a payment status transition. Available for test-coin assets only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.CryptopaySimulatePaymentRequest{
        PaymentID: "paymentId",
    }
client.Payments.SimulatePayment(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**paymentID:** `string` — Payment ID
    
</dd>
</dl>

<dl>
<dd>

**amount:** `*string` — Optional simulated received amount, integer string in the asset's smallest unit (see CreatePaymentRequest.amount).
    
</dd>
</dl>

<dl>
<dd>

**status:** `*suwardsdkgo.CryptopayPaymentStatusEnum` — Target main status. Required — status and subStatus are independent axes, both must be supplied.
    
</dd>
</dl>

<dl>
<dd>

**subStatus:** `*suwardsdkgo.CryptopayPaymentSubStatusEnum` — Target sub-status (amount/detail axis). Required — status and subStatus are independent axes, both must be supplied.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.QuotePaymentFees(request) -> *suwardsdkgo.CryptopayQuotePaymentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the platform fee, estimated network fee, and net amount for a payment of `amount` in `asset`, without creating anything. All monetary fields are integer strings in the asset's smallest unit.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.CryptopayQuotePaymentRequest{
        Asset: suwardsdkgo.CryptopayAssetIDUsdtEthereum,
        Amount: "amount",
    }
client.Payments.QuotePaymentFees(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**asset:** `*suwardsdkgo.CryptopayAssetID` — Asset identifier (see GET /v1/assets for the live list).
    
</dd>
</dl>

<dl>
<dd>

**amount:** `string` — Merchant base amount, integer string in the asset's smallest unit. Example: "5000000" = 5 USDT. The response returns the derived gross (what the customer pays) and netAmount (what the merchant receives).
    
</dd>
</dl>

<dl>
<dd>

**networkFeePayer:** `*suwardsdkgo.CryptopayFeePayer` — Who bears the network (gas) fee. Default merchant.
    
</dd>
</dl>

<dl>
<dd>

**serviceFeePayer:** `*suwardsdkgo.CryptopayFeePayer` — Who bears the platform (service) fee. Default merchant.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Payments.ListPaymentTransactions(PaymentID) -> *suwardsdkgo.CryptopaywireTransactionList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Paginated list of the on-chain transactions detected for a payment.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1PaymentsPaymentIDTransactionsRequest{
        PaymentID: "paymentId",
    }
client.Payments.ListPaymentTransactions(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**paymentID:** `string` — Payment ID
    
</dd>
</dl>

<dl>
<dd>

**order:** `*suwardsdkgo.GetV1PaymentsPaymentIDTransactionsRequestOrder` — Sort order by id: asc = ascending, anything else = descending
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Page size (default 20, max 100)
    
</dd>
</dl>

<dl>
<dd>

**lastID:** `*string` — Pagination cursor: last id from the previous page
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## StaticWallets
<details><summary><code>client.StaticWallets.ListStaticWallets() -> *suwardsdkgo.CryptopayListStaticWalletsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the project's static wallets, newest first. Paginated via limit and lastId.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1StaticWalletsRequest{}
client.StaticWallets.ListStaticWallets(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order:** `*suwardsdkgo.GetV1StaticWalletsRequestOrder` — Sort order (asc/desc)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Limit (default 20, max 100)
    
</dd>
</dl>

<dl>
<dd>

**lastID:** `*string` — Last ID for pagination
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.CreateStaticWallet(request) -> *suwardsdkgo.CryptopayStaticWalletResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a reusable deposit address with an accepted-asset allow-list
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.CryptopayCreateStaticWalletRequest{}
client.StaticWallets.CreateStaticWallet(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**allowedAssets:** `[]*suwardsdkgo.CryptopayAssetID` — Accepted-asset allow-list, as asset id-strings (see GET /v1/assets), e.g. ["USDT_ARBITRUM"]. Deposits of assets not on this list are ignored (status "ignored") and not credited.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Your own identifier for this static wallet. Echoed back on the wallet and denormalized onto each of its deposits. Optional.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `map[string]any` — Arbitrary JSON key/value data to attach to the static wallet. Stored and echoed back unchanged.
    
</dd>
</dl>

<dl>
<dd>

**webhookURL:** `*string` — Webhook URL to receive this wallet's deposit events. Optional; falls back to the project default webhook when omitted.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.GetStaticWallet(StaticWalletID) -> *suwardsdkgo.CryptopayStaticWalletResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetch a single static wallet by its id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1StaticWalletsStaticWalletIDRequest{
        StaticWalletID: "staticWalletId",
    }
client.StaticWallets.GetStaticWallet(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**staticWalletID:** `string` — Static wallet ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.DeleteStaticWallet(StaticWalletID) -> map[string]bool</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a static wallet. Its address stops being monitored and can no longer receive new deposits; previously recorded deposits are unaffected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.DeleteV1StaticWalletsStaticWalletIDRequest{
        StaticWalletID: "staticWalletId",
    }
client.StaticWallets.DeleteStaticWallet(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**staticWalletID:** `string` — Static wallet ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.UpdateStaticWallet(StaticWalletID, request) -> *suwardsdkgo.CryptopayStaticWalletResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update a static wallet's accepted-asset allow-list, metadata, or webhook URL. Only the fields present in the body are changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.CryptopayUpdateStaticWalletRequest{
        StaticWalletID: "staticWalletId",
    }
client.StaticWallets.UpdateStaticWallet(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**staticWalletID:** `string` — Static wallet ID
    
</dd>
</dl>

<dl>
<dd>

**allowedAssets:** `[]*suwardsdkgo.CryptopayAssetID` — New accepted-asset allow-list, as asset id-strings (see GET /v1/assets). When empty or omitted the current list is left unchanged.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `map[string]any` — Replacement key/value metadata for the static wallet.
    
</dd>
</dl>

<dl>
<dd>

**webhookURL:** `*string` — Replacement webhook URL for this wallet's deposit events.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.ListStaticWalletDeposits(StaticWalletID) -> *suwardsdkgo.CryptopayListStaticDepositsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Paginated list of the deposits received by a static wallet, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1StaticWalletsStaticWalletIDDepositsRequest{
        StaticWalletID: "staticWalletId",
    }
client.StaticWallets.ListStaticWalletDeposits(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**staticWalletID:** `string` — Static wallet ID
    
</dd>
</dl>

<dl>
<dd>

**order:** `*suwardsdkgo.GetV1StaticWalletsStaticWalletIDDepositsRequestOrder` — Sort order (asc/desc)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Limit (default 20, max 100)
    
</dd>
</dl>

<dl>
<dd>

**lastID:** `*string` — Last ID for pagination
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.GetStaticWalletDeposit(StaticWalletID, DepositID) -> *suwardsdkgo.CryptopayStaticDepositResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetch a single static-wallet deposit by its id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.GetV1StaticWalletsStaticWalletIDDepositsDepositIDRequest{
        StaticWalletID: "staticWalletId",
        DepositID: "depositId",
    }
client.StaticWallets.GetStaticWalletDeposit(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**staticWalletID:** `string` — Static wallet ID
    
</dd>
</dl>

<dl>
<dd>

**depositID:** `string` — Deposit ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.StaticWallets.SimulateStaticWalletDeposit(StaticWalletID, request) -> *suwardsdkgo.CryptopayStaticDepositResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Drive a synthetic deposit through its lifecycle (no on-chain activity, no balance credit). Available for test-coin assets only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &suwardsdkgo.CryptopaySimulateStaticDepositRequest{
        StaticWalletID: "staticWalletId",
    }
client.StaticWallets.SimulateStaticWalletDeposit(
        context.TODO(),
        request,
    )
}
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**staticWalletID:** `string` — Static wallet ID
    
</dd>
</dl>

<dl>
<dd>

**amount:** `*string` — Deposited amount to simulate, an integer string in the asset's smallest unit (see CreatePaymentRequest.amount).
    
</dd>
</dl>

<dl>
<dd>

**asset:** `*suwardsdkgo.CryptopayAssetID` — Asset id-string of the simulated deposit (see GET /v1/assets), e.g. USDT_ARBITRUM.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*suwardsdkgo.CryptopaySimulateStaticDepositRequestStatus` — Target lifecycle stage to drive the simulated deposit to.
    
</dd>
</dl>

<dl>
<dd>

**transferIndex:** `*string` — Optional index of the transfer within the transaction, as a string-encoded integer.
    
</dd>
</dl>

<dl>
<dd>

**txHash:** `*string` — Optional synthetic transaction hash; a random one is generated when omitted.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Assets
<details><summary><code>client.Assets.ListAcceptedAssets() -> *suwardsdkgo.GetV1AssetsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all assets accepted by the Suward gateway. No authentication required.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Assets.ListAcceptedAssets(
        context.TODO(),
    )
}
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Assets.ListSupportedBlockchains() -> []*suwardsdkgo.CryptopayBlockchainResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all supported blockchains (informational). No authentication required.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Assets.ListSupportedBlockchains(
        context.TODO(),
    )
}
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

