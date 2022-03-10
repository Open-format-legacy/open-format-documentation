# Read from the subgraph

### Code

Let's go back into our [whitelabel-starter](https://github.com/simpleweb/whitelabel-starter) project from the [Create a release](../the-factory/create-a-release.md) section and add a file called `subgraph.js`. Add the following code to the file:

```
const { gql, request } = require("graphql-request");

async function main() {
 // The graphql query with the data we want to fetch from the subgraph
  const query = gql`
    {
      mediaItems {
        id
        factory_id
        metadata {
          key
          value
        }
      }
    }
  `;

  await request(
    "https://api.thegraph.com/subgraphs/name/tinypell3ts/music-factory",
    query
  )
    .then((data) => console.log(JSON.stringify(data, null, "\t")))
    .catch((err) => console.log(err));
}

main();
```

Save the file and run node `subgraph.js`. You should see a list of `mediaItems` logged in your console.&#x20;

```
{
        "mediaItems": [
                {
                        "id": "0x1424f09a10f5b480bd27421afbaf52ecc5a275ac",
                        "factory_id": null,
                        "metadata": [
                                {
                                        "key": "artist",
                                        "value": "Redeye"
                                },
                                {
                                        "key": "audio",
                                        "value": "ipfs://bafybeiecgkosheubgexdeupvhulnsaothrlpg76tflqnuaejg5yfqrpiji/DarkAngel.mp3"
                                },
                                {
                                        "key": "description",
                                        "value": "Ancient D&B test that's now very desirable."
                                },
                                {
                                        "key": "image",
                                        "value": "ipfs://bafybeidu26lz3t6fk4f5jcj53vwzsvhc7bxmjtdpj4ahq3heo6q5tqrseq/WL.jpg"
                                },
                                {
                                        "key": "name",
                                        "value": "Dark Angel"
                                }
                        ]
                },
```

Now let's find your release. You will need the contract address of your release. You can get this from [PolygonScan (Mumbai) explorer](https://mumbai.polygonscan.com).&#x20;

![](<../../.gitbook/assets/Screenshot 2022-03-10 at 09.55.30.png>)

Now let's go back into the `subgraph.js` file and slightly amend our main function. We need to pass our contract address from the request into our query. Replace the **`id`** below with your contract address (release id).&#x20;

```
async function main() {
  // The graphql query with the data we want to fetch from the subgraph
  const query = gql`
    query ($id: String!) {
      mediaItem(id: $id) {
        id
        factory_id
        metadata {
          key
          value
        }
      }
    }
  `;

  await request(
    "https://api.thegraph.com/subgraphs/name/tinypell3ts/music-factory",
    query,
    { id: "0x509dbec44331e44749ae80a4e0c27a7c16aefb57" } // replace this ID
  )
    .then((data) => console.log(JSON.stringify(data, null, "\t")))
    .catch((err) => console.log(err));
}
```

Save the file and run `node subgraph.js`. You should now only see your release logged in the console.&#x20;

```
{
        "mediaItem": {
                "id": "0x509dbec44331e44749ae80a4e0c27a7c16aefb57",
                "factory_id": null,
                "metadata": []
        }
}
```

Congratulations! Now go build something awesome!&#x20;

If you need any help or want to show off what you're building, join us on [Discord](https://discord.com/invite/MZe9cRQcVt)!
