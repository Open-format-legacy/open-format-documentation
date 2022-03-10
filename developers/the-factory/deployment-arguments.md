# Deployment Arguments

#### Payees : Array

The Payees is a list of ethereum addresses that you wish to share all release earnings with.  Each address in `payees` is assigned the number of shares at the matching position in the `shares` array.

**Shares : Array**

An Array of shares for each payees. 1 share = 1%. A maximum of 100 shares can be allocated.&#x20;

**Sale Price: BigNumber**

The cost to mint each release. This number is in Wei. We recommend using `ethers.utils.parseEther("<amount>").`

**Name : String**\
****The name is the name of the release.

**Symbol: String**

The ERC721 token symbol for the release. This is generally a three or four word capitalised string. e.g. TOON, SONG, BTC, ETH

**Quantity: Number**

The number of release that can be minted from the release.&#x20;

**Royalties Percentage: Number**

Royalties are how much the payees earn for each sale of the release on the secondary market. The number is between 0 - 10000. e.g 2.5% = 250, 50% = 5000. We're using the[ EIP-2981: NFT Royalty Standard](https://eips.ethereum.org/EIPS/eip-2981) to handle royalty calculations.&#x20;

**Metadata** **URL: String**

A url that links to the metadata for the release. The format follows the [OpenSea Metadata Standards](https://docs.opensea.io/docs/metadata-standards#metadata-structure). Example:

```
{
    "name": "My new track", 
    "description": "This is my new track",
    "release_type": "audio",
    "factory_id": "9fe76381-8c02-4f41-9e74-05f438bf2e22",
    "image": "ipfs://bafybeidds6bbciwxrjtwykuustiyxag5l3asdu4ddgx5hk3v7ytdwshyum/Blink-182_-_All_the_Small_Things_cover.jpeg",
    "audio": "ipfs://bafybeiajpwppsxvigi3q7b4gnc7mlbvo5dgpmkntivgdf4ekh4xfyprtbm/file_example_MP4_1920_18MG.mp4"
    "attributes": [
      {
        "trait_type": "BPM", 
        "value": "180"
      }, 
      {
        "trait_type": "Genre", 
        "value": "techno"
      }, 
      {
        "trait_type": "Mouth", 
        "value": "Surprised"
      }, 
}
```

#### Metadata - Best Practises

* If you're creating your own frontend factory you may only want to display releases that are created in your factory on your marketplace. Adding a `factory_id` identifier will allow you to filter the subgraph to only display releases created from a certain factory. You can see an example in the [fetching release data](../the-subgraph/read-from-the-subgraph.md) section.
* The `release_type` should be either `"video"` or `"audio"`. This will help with indexing, filtering and searching data.&#x20;
* The keys and values of the attributes should be formatted to lowercase and words joined with a hyphen. e.g `drum-and-bass`, `drum-machine`

