# ICFoxy (soMINT): Motoko Bootcamp project 

[I'm an inline-style link with title](https://j76pn-raaaa-aaaai-qicmq-cai.raw.ic0.app/ "Google's Homepage")

This is a basic NFT minter inspired by the DIP 721 standard (implementation not guarantee, consider this example as an educational ressource. For a production project with DIP721, please take a look at the official DIP721 repo).

![Login](https://github.com/hboshnak/raw/master/pics/login.png "Login view")

![Logged](https://github.com/hboshnak/raw/master/pics/logged.png "Logged view")

![Minted](https://github.com/hboshnak/raw/master/pics/minted.png "Minted view")

Before proceeding it's good to get acquainted with:

- [Quick Start](https://sdk.dfinity.org/docs/quickstart/quickstart-intro.html)
- [SDK Developer Tools](https://sdk.dfinity.org/docs/developers-guide/sdk-guide.html)
- [Motoko Programming Language Guide](https://sdk.dfinity.org/docs/language-guide/motoko.html)
- [Motoko Language Quick Reference](https://sdk.dfinity.org/docs/language-guide/language-manual.html)
- [JavaScript API Reference](https://erxue-5aaaa-aaaab-qaagq-cai.raw.ic0.app)


## Running the project locally

If you want to test your project locally, you can use the following commands:


Select a folder in your directory and clone the project
```bash
mkdir motoko
cd motoko
git clone https://github.com/hboshnak/soMINT
cd soMINT
```

It's assumed that you're fullfilled the prerequisites ( as dfx for e.g.)
Just in case, start with a stop. It'll not hurt
```bash
dfx stop
```
Starts a clean local replica
```bash
dfx start --clean
```
There are some issues due to the different dfx versions.
I solve them like that
```bash
export NODE_OPTIONS=--openssl-legacy-provider
```
After that we need to install the npm modules
```bash
npm i
```
Now we're goot to go deploy the canisters locally, be creative with the names.
This deploys your canisters to the local replica and generates your candid interface
```bash
dfx deploy --argument '("somint","SMNT")'
```
Now we can start also the npm services
```bash
npm run start
npm start
```
Once the job completes, your application will be available at `http://localhost:8000?canisterId={asset_canister_id}`.
Here is where your replica lives.
```bash
dfx deploy --argument '("somint","SMNT")'
```
is needed to rebuild and see the changes you made
Additionally, if you are making frontend changes, you can start a development server with

```bash
npm start
```

Which will start a server at `http://localhost:8080`, proxying API requests to the replica at port 8000.
If changes are satisfying just redeploy the dfx

#WEN MAINNET?

If you want to go live do the following steps
Again just in case... upgrade your wallet
```bash
dfx wallet --network ic upgrade
dfx canister --network ic --wallet "$(dfx identity --network ic get-wallet)" update-settings --all --add-controller "$(dfx identity get-principal)"
```
Short pray and... we go live over ICP
```bash
dfx deploy --network ic --argument '("ICFoxy","ICFX")'
```


### Note on frontend environment variables

If you are hosting frontend code somewhere without using DFX, you may need to make one of the following adjustments to ensure your project does not fetch the root key in production:

- set`NODE_ENV` to `production` if you are using Webpack
- use your own preferred method to replace `process.env.NODE_ENV` in the autogenerated declarations
- Write your own `createActor` constructor
