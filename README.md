# Blog accessibilité

## Test

```bash

# clone the repo
git clone https://github.com/RodolpheANDRIEUX/Accessibility-B2.git
cd Accessibility-B2/

# install dependencies
npm install

# start the server in the background
npm run dev -- --open &

# wait for the server to start
sleep 3

# use unlighthouse to scrap the whole website
npx unlighthouse --site http://localhost:5173/ --desktop

# you might want to install node if you dont have it yet 
# and npm with "npm install -g npm"

```

> The performance score isn't acurate with unlighthouse, you will have to use lighthouse in the browser.