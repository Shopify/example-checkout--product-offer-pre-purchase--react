# Checkout UI Extension

Checkout UI extensions let app developers build custom functionality that merchants can install at defined targets in the checkout flow. You can learn more about checkout UI extensions in Shopify’s [developer documentation](https://shopify.dev/api/checkout-extensions/checkout).


## Prerequisites
Make sure to complete [all the prerequisites](https://shopify.dev/apps/checkout/delivery-instructions/getting-started#requirements) from any tutorials to develop a Checkout UI extension.

## Tutorials
The best way to get started is to follow some of the available Extension Tutorials:

For creating an extension:
* [Enable extended delivery instructions](https://shopify.dev/apps/checkout/delivery-instructions)
* [Adding product offer recommendations](https://shopify.dev/apps/checkout/product-offers)
* [Creating a custom banner](https://shopify.dev/apps/checkout/custom-banners)

To add specific features to an extension
* [Adding field validation](https://shopify.dev/apps/checkout/validation)
* [Localizing an extension](https://shopify.dev/apps/checkout/localize-ui-extensions)

## Getting Started
Initially, your extension will have the following files:

```
└── my-app
  └── extensions
    └── my-checkout-ui-extension
        ├── src
        │   └── PurchaseCheckoutBlockRender.jsx The source code for the `purchase.checkout.block.render` extension target
        ├── locales
        │   ├── en.default.json // The default locale for the checkout UI extension. Shared across all extension targets.
        │   └── fr.json // The locale file for non-regional French translations. Shared across all extension targets.
        └── shopify.extension.toml // The config file for the checkout UI extension

```

You can customize your new extension by editing the code in the `src/PurchaseCheckoutBlockRender.jsx` file.

> By default, your extension is configured to target the `purchase.checkout.block.render` [extension target](https://shopify.dev/docs/api/checkout-ui-extensions/extension-targets-overview). This extension target does not have a single location in the checkout where it will appear; instead, a merchant installing your extension will configure where *they* want your extension to show up.
> If you are building an extension that is tied to existing UI element in the checkout, such as the cart lines or shipping method, you can change the extension target so that your UI extension will render in the correct location. Check out the list of [all available extension targets](https://shopify.dev/docs/api/checkout-ui-extensions/extension-targets-overview) to get some inspiration for the kinds of content you can provide with checkout UI extensions.

You can add new extension targets by adding a new entry to `src/shopify.extension.toml`, e.g:

```` toml
[[extensions.targeting]]
target = "purchase.checkout.cart-line-item.render-after"
module = "./src/CheckoutCartLinesRenderAfter.jsx"
````

You would then add a new file at `src/CheckoutCartLinesRenderAfter.jsx`.

To shape your extension you have the following collection of tools available:

* [Checkout UI components](https://shopify.dev/docs/api/checkout-ui-extensions/components), the visual elements you can render in your checkout extension targets.
* Admin UI Extensions for [React](https://github.com/Shopify/ui-extensions/tree/main/packages/admin-ui-extensions-react) & [JavaScript](https://github.com/Shopify/ui-extensions/tree/main/packages/admin-ui-extensions)
* [Extension APIs](https://shopify.dev/docs/docs/api/checkout-ui-extensions/apis/extensiontargets), which give you access to read and write data in the checkout.

> If you are using React, there is also a large collection of [React Hooks available](https://shopify.dev/docs/api/checkout-ui-extensions/react-hooks) to ease access to these operations, otherwise you'll need to manually subscribe to the subscribable value directly with a callback.

## FAQ
* **How can I switch my extension between static and dynamic?**

  1. Make sure you've started your local development server using `npm|yarn|pnpm dev`
  2. Depending on your selected location they may be either `dynamic` or `static` extension targets, which diferr slightly on the process to preview them.
      - `Dynamic extensions` can be placed using a [query string parameter](https://shopify.dev/apps/checkout/test-ui-extensions#dynamic-extension-targets).
      - `Static extensions` require no extra work, just note that a static extension is shown only if the section that they are attached to is enabled.

* **How can I change my extension type?**

    To change your extension type, be mindful that you have to change it in the following places:
    1. In your `script file`, where you declared the extension (will be either _render()_ or _extend()_), you'll have to change the declared extension target.
    2. In your `settings TOML file` (shopify.extension.toml) you'll have to change the `[[extensions.targeting]]` declaration for your new desired target.

* **How do I let merchants customize my extension?**

    You can enable merchants to customize your extension through the [checkout ui extension settings](https://shopify.dev/docs/api/checkout-ui-extensions/configuration#settings-definition) which define a set of fields and values that the merchant can set from the checkout editor. You can use validation options to apply additional constraints to the data that the setting can store, such as a minimum or maximum value.

    To learn more, you can follow the step-by-step process in the tutorial to [add a custom banner](https://shopify.dev/apps/checkout/custom-banners/add-custom-banner).

## Useful Links

- [Checkout app documentation](https://shopify.dev/apps/checkout)

- [Checkout UI extension documentation](https://shopify.dev/api/checkout-extensions)
  - [Configuration](https://shopify.dev/docs/api/checkout-ui-extensions/configuration)
  - [API Reference](https://shopify.dev/docs/api/checkout-ui-extensions/apis)
  - [UI Components](https://shopify.dev/docs/api/checkout-ui-extensions/components)
  - [Available React Hooks](https://shopify.dev/docs/api/checkout-ui-extensions/react-hooks)
