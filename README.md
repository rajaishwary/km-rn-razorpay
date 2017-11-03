# react-native-razorpay
[![npm](https://img.shields.io/npm/l/express.svg)]()

[![NPM](https://nodei.co/npm/react-native-razorpay.png?downloads=true)](https://nodei.co/npm/react-native-razorpay/)

React Native wrapper around our Android and iOS mobile SDKs

To know more about Razorpay payment flow and steps involved, please read up here:
<https://docs.razorpay.com/docs>

## Installation

This has 3 steps: add to project, installation and linking iOS SDK.

### Add to project

Run the following on terminal from your project directory:

```bash
$ npm i react-native-razorpay --save
```

### Automatic installation

```bash
$ react-native link react-native-razorpay
```

##### Manual installation

If the above command doesn't work for you (installation), try [these steps from wiki][wiki].

### Additional Steps for Linking iOS SDK

React Native creates static library for each plugin / library / framework / native module being used.

Due to some limitation on the way Xcode links static and dynamic
libraries / frameworks to projects, we require some additional
steps to be followed to link our iOS SDK to the React Native project.

You can skip steps 1, 2 and 3 if you used `npm`.

1. Download [Razorpay's iOS SDK from here][ios-docs] and unzip it.
2. Delete the `.framework` file from
`path/to/your/project/node_modules/react-native-razorpay/ios`.
3. Copy the `.framework` file obtained in step 1 to
`path/to/your/project/node_modules/react-native-razorpay/ios`.
4. Open `path/to/your/project/ios/<your_project>.xcworkspace` or
`path/to/your/project/ios/<your_project>.xcodeproj`
5. Also link the `.framework` file **_directly_ to your project** in Xcode. Check the
 `Copy items if needed` box and select your project target from the list below.
6. Add the following line of code in your `AppDelegate.m` under the imports section:  
`#import <dlfcn.h>`
7. Add the following line of code in your `AppDelegate.m` inside the
`application:didFinishLaunchingWithOptions:` method:  
`dlopen("Razorpay.framework/Razorpay", RTLD_LAZY | RTLD_GLOBAL);`

## Usage

Sample code to integrate with Razorpay can be found in
[index.js][index.js] in the included example directory.

To run the example, simply do the following in example directory and then
link iOS SDK as explained in the previous section:

`$ npm i`

### Steps

1. Import RazorpayCheckout module to your component:
    ```js
    import RazorpayCheckout from 'react-native-razorpay';
    ```

2. Call `RazorpayCheckout.open` method with the payment `options`. The method
returns a **JS Promise** where `then` part corresponds to a successful payment
and the `catch` part corresponds to payment failure.
    ```js
    <TouchableHighlight onPress={() => {
      var options = {
        description: 'Credits towards consultation',
        image: 'https://i.imgur.com/3g7nmJC.png',
        currency: 'INR',
        key: 'rzp_test_1DP5mmOlF5G5ag',
        amount: '5000',
        name: 'foo',
        prefill: {
          email: 'akshay@razorpay.com',
          contact: '8955806560',
          name: 'Akshay Bhalotia'
        },
        theme: {color: '#F37254'}
      }
      RazorpayCheckout.open(options).then((data) => {
        // handle success
        alert(`Success: ${data.payment_id}`);
      }).catch((error) => {
        // handle failure
        alert(`Error: ${error.code} | ${error.description}`);
      });
    }}>
    ```

A descriptive [list of valid options for checkout][options] is available (under
Manual Checkout column).

## Contributing

See the [CONTRIBUTING] document. Thank you, [contributors]!

## License

react-native-razorpay is Copyright (c) 2016 Razorpay Software Pvt. Ltd.
It is distributed under [the MIT License][LICENSE].

We ♥ open source software!
See [our other supported plugins / SDKs][integrations]
or [contact us][contact] to help you with integrations.

[contact]: mailto:integrations@razorpay.com?subject=Help%20with%20React%20Native "Send us a mail"
[CONTRIBUTING]: CONTRIBUTING.md "Our contributings guidelines"
[contributors]: https://github.com/razorpay/react-native-razorpay/graphs/contributors "List of contributors"
[index.js]: example/index.js "index.js"
[integrations]: https://razorpay.com/integrations "List of our integrations"
[ios-docs]: https://docs.razorpay.com/v1/page/ios-integration "Documentation for the iOS Integration"
[LICENSE]: /LICENSE "MIT License"
[options]: https://docs.razorpay.com/docs/checkout-form#checkout-fields "Checkout Options"
[wiki]: https://github.com/razorpay/react-native-razorpay/wiki/Manual-Installation
