# Create a release

### **Steps:**

* Visit the [whitelabel factory](https://whitelabel-factory.netlify.app) and connect your wallet with [Metamask](https://metamask.io). The whitelabel factory currently uses [Polygon](https://polygon.technology) Mumbai testnet.&#x20;

{% hint style="info" %}
You can get free MATIC for testing at [https://faucet.polygon.technology/](https://faucet.polygon.technology)
{% endhint %}

{% embed url="https://user-images.githubusercontent.com/7047410/156161902-b17ea881-cfa2-40a5-8d48-d9f31125f15f.mp4" %}
Connect your wallet
{% endembed %}

* In the Assets table you can upload audio, artwork and licence (optional) for your release. Currently we're only accepting .mp3 as the format for the audio. We will be adding functionality to upload different audio qualities.
* Once uploaded you will see a preview of the audio and artwork.
* Next, Add an **Artist Name**, **Track name**, and **Track Description**. A **Blockchain track identifier** is also required. This identifier helps track your release on the blockchain.
* You can now add attributes. Attributes have a type and a value. They're useful as they help find your release when filtering and searching the platform. All attribute values are formatted.

![Attributes](<../../.gitbook/assets/Screenshot 2022-03-01 at 11.49.18.png>)

* Once you've added some attributes, you can now add a **Quantity** and **Sale Price**. The quantity is the maximum number of releases that can be minted. The sale price by default is in [MATIC](https://decrypt.co/resources/what-is-polygon-matic-and-why-it-matters-for-ethereum), which is the default currency for the Polygon Network. We convert the inputted sale price into GBP based on the latest MATIC/GBP conversion rate.

![Quantity and sale price](<../../.gitbook/assets/Screenshot 2022-03-01 at 11.50.35.png>)

* As you can see in the preview image, you can also **Add royalties** and **Add splits.**
* Toggle **Add royalties** to display the royalties tab.&#x20;

![Add Royalties](<../../.gitbook/assets/Screenshot 2022-03-01 at 11.50.45.png>)

* The royalty percentage is a percentage of the sale price on any secondary sale. For example. If you set the royalty percentage to 10% and John mints your release and then sells it to Jane for 10 MATIC, you will receive 1 MATIC and John will receive 9 MATIC. This number can be to two decimals places.&#x20;
* Next, you can add splits. Toggle **Add splits** to display the splits tab.&#x20;

![Splits](<../../.gitbook/assets/Screenshot 2022-03-01 at 11.51.34.png>)

* Splits are a way you can share earnings between multiple parties. You need to know the ethereum address of the party you wish to share your earnings with. You can add as many splits as you like, but can only allocate a maximum of 100 shares. **Each share is equal to 1% of any release earnings**. These earnings come from primary sales and secondary sale royalties (if set).&#x20;
* Please note, the earnings are not automatically released on each sale. It needs to be trigger in the [Release Dashboard](view-releases.md) by the creator.&#x20;
