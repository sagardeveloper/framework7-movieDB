# framework7-movieDB

### Install the project
```
clone repository from "https://github.com/sagardeveloper/framework7-movieDB.git"

for example: git clone https://github.com/sagardeveloper/framework7-movieDB.git
### OR

Download the project directlly by clicking "Clone or Download"
 - Run npm Command in the project "npm install or npm i"
 ** **
 
```

### Crearte an movie API
You need the movie db api before running this application:

- Go to "https://www.themoviedb.org/"
- Sign-up if you don't have account
- Go to your profile setting 
- Click on the API from left panel and create your secret API key

## Usage

> Config api.js file

> Go to src **assets > js > api.js

```
const key="paste your movie db api key here";
export default key;
```
### Running the Applications
```
check the platform by running this command > "cordova platform"
- Run app on the browser by:
   cordova run browser -- --lr
 
- Run app on the Android Device:
   cordova run android 
 
- Run app on the IOS Device:
   cordova run ios

```
