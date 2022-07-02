```js
// `source` is obtained with Stripe.js; see https://stripe.com/docs/payments/accept-a-payment-charges#web-create-token
const charge = await stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
  description: 'My First Test Charge (created for API docs at https://www.stripe.com/docs/api)',
});
```

> source optional
> A payment source to be charged. This can be the ID of a card (i.e., credit or debit card), a bank account, a source, a token, or a connected account. For certain sources—namely, cards, bank accounts, and attached sources—you must also pass the ID of the associated customer.



驗證規則和結果
有提供cvc、住家地址、住家zip
> ### Verification responses

> If the `cvc` parameter is provided, Stripe will attempt to check the correctness of the CVC, and will return this check's result. Similarly, if `address_line1` or `address_zip` are provided, Stripe will try to check the validity of those parameters.

> Some card issuers do not support checking one or more of these parameters, in which case Stripe will return an `unavailable` result.

> Also note that, depending on the card issuer, charges can succeed even when passed incorrect CVC and address information.

檢查卡號是否正確、是否過期。
> Returns the charge object if the charge succeeded. This call will throw [an error](https://stripe.com/docs/api/charges/create#errors) if something goes wrong. A common source of error is an invalid or expired card, or a valid card with insufficient available balance.

https://github.com/WebDevSimplified/Node.js-Stripe-Shopping-Cart/blob/master/server.js

剩下研究至Develop/webDevelop下