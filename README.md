Table of Contents
=================

   * [Running the blockchain locally](#running-the-blockchain-locally)
   * [Run FrontEnd Mobile Application locally](#run-frontEnd-mobile-application-locally)
   * [Deploying to IBM Cloud as a Cloud Foundry application](#deploying-to-ibm-cloud-as-a-cloud-foundry-application)
   * [Cors issue fix](#cors-issue-fix)
   * [Docker Support](#docker-support)
   * [Tendermint Api Documentation](#tendermint-api-documentation)


## Tendermint Blockchain Chat App
![Tendermint](http://www.peerity.io/images/Tendermint-logo2.png)

This is minimal chat application based on Tendermint Consensus Engine using Lotionjs. It also includes web/mobile application built using Ionic 3.

### Running the blockchain locally
1. Navigate to blockchain dir 
```
$ cd cf
```
2. Install dependencies 
```
$ npm i 
```
3. Run the Blockchain
``` 
$ node app.js
```

![3](img/3.png)

Your tendermint port is 46667

1. Endpoint: http://localhost:8080/get (GET), shows current data in blockchain
2. Endpoint: http://localhost:8080/post (POST), post new data in blockchain
3. Endpoint: http://localhost:46657/ , access available Apis provided by Tendermint RPC 

![4](img/4.png)

End points available through ABCI (Application blockchain interface) :)

How simple can that be?

## Run FrontEnd Mobile Application locally
1. Navigate to frontend dir
```
$ cd frontend
```
2. Install dependencies
```
$ npm i
```
3. Install ionic cli 
```
$ npm i -g ionic cordova
```
4. Run the app
```
$ ionic serve
```
5. App running on port 8100
```
http://localhost:8100
```
## CORS Issue Fix 
If you face error as such 
![error](img/error.png)

1. Install "Allow-Control-Allow-Origin: *" plugin of google chrome to enable CORS

link: [Allow-Control-Allow-Origin: *](https://chrome.google.com/webstore/detail/allow-control-allow-origi/nlfbmbojpeacfghkpbjhddihlkkiljbi?hl=en)

2. Enable CORS 
![cors](img/cors.png)

## Docker Support 
1. Navigate to blockchain directory
```
$ cd blockchain
```
2. Build image from Dockerfile
```
$ docker build -t tendermint .
```
3. Run Dockerfile
```
$ docker run -p 8080:8080 -p 46657:46657 -d tendermint:latest
```
4. See the running container
```
$ docker ps
```
5. Stop the container
```
$ docker stop containerid
``` 
6. Remove Container
```
$ docker rm containerid
```

## Screenshot of App

![5](img/5.png)


![6](img/6.png)


![7](img/7.png)


![8](img/8.png)

## Deploying to IBM Cloud as a Cloud Foundry application
1. Signup to [IBM Cloud](https://console.bluemix.net/registration/)
2. Install [Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
3. Open ```manifest.yml``` and give app a name
4. Open command line and type 
```
$ cf login -a https://api.ng.bluemix.net -u <ibm.com id>
``` 
5. Navigate to ```cf``` directory 
```
$cd cf
```
6. Push the Application to IBM Cloud
```
$ cf push
```
7. Copy the URL generated Cloud Foundry
8. Open ```frontend/src/pages/congif/config.ts``` , and change the baseurl to the url you copied.
9. Navigate to frontend dir
```
$ cd frontend
```
10. Build the production ready web app by ionic cli
```
$ ionic cordova build browser
```
11. Navigate to ```frontend/platforms/browser```. Copy ```www``` folder and paste in ```cf``` folder
12. Push the app, this will have a fully functional Blockchain with a sexy frontend build with ionic <3
```
$ cf push
```
13. URL generated by cloud foundry is your application

## Tendermint Api Documentation
| Endpoint      | Type          | Payload|
| ------------- |:-------------:| -----:|
| /api/get    | GET | - |
| /api/abci_info    | GET | - |
| /api/dump_consensus_state     | GET      |   - |
| /api/genesis | GET      |    - |
| /api/net_info | GET   |    -|
| /api/num_unconfirmed_txs| GET     |   - |
| /api/status| GET     |    - |
| /api/unconfirmed_txs | GET     |   - |
| /api/abci_query | POST      |    {"path":"","data":"","height":0,"prove":""} |
| /api/block |POST     |    {"height":0} |
| /api/block_results |POST      |     {"height":0} |
| /api/blockchain| POST      |    {"minHeight":0,"maxHeight":100} |
| /api/broadcast_tx_async|POST     |    {"tx":""}|
| /api/broadcast_tx_commit | POST     |    {"tx":""} |
| /api/broadcast_tx_sync | POST      |    {"tx":""} |
| /api/commit |POST    |     {"height":0}|
| /api/subscribe |POST      |    {"query":""} |
| /api/tx | POST      |    {"hash":"","prove":""}  |
| /api/tx_search' | POST     |    {"query":"","prove":""} |
| /api/post    | POST | {"sender":"","message":""} |