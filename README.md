# hibp-treeshaking-test

> This project was bootstrapped with
> [Create React App](https://github.com/facebook/create-react-app).

### Premise

[`hibp`](https://github.com/wKovacs64/hibp) exports several functions. One of
them, `pwnedPassword`, depends on the
[`jssha`](https://github.com/Caligatio/jsSHA) library, but others (e.g.
`dataClasses`) do not. Therefore, importing only `dataClasses` should not cause
`jssha` to end up in the final bundle.

### The Test

Run

```
yarn build
```

Then, the following command:

```
grep "Chosen SHA variant is not supported" build/static/js/*.js
```

...should find nothing as this text comes from `jssha` and the example code is
only importing the `dataClasses` function. If it does find something, that means
`jssha` is in the bundle, which is bad.
