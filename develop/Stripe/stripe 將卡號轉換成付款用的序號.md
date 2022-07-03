

>#### stripe.createToken(cardElement, data?)
>Use `stripe.createToken` to convert information collected by card elements into a single-use [Token](https://stripe.com/docs/api#tokens) that you safely pass to your server to use in an API call.



```js
stripe.createToken(cardElement).then(function(result) {
  // Handle result.error or result.token
});
```

The `card` [Element](https://stripe.com/docs/js/tokens_sources/create_token?type=cardElement#element_intro) you wish to tokenize data from. If applicable, the `Element` tokenizes by pulling data from other elements you’ve created on the same instance of [Elements](https://stripe.com/docs/js/tokens_sources/create_token?type=cardElement#elements_create)—you only need to supply one `Element` as the parameter.



> ## Returns

> `stripe.createToken` returns a `Promise` which resolves with a `result` object. This object has either:
> -   `result.token`: a [Token](https://stripe.com/docs/api/tokens) was created successfully.
> -   `result.error`: there was an error. This includes client-side validation errors. Refer to the [API reference](https://stripe.com/docs/api#errors) for all possible errors.