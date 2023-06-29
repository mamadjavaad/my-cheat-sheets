# Puppeteer Cheat Sheet

## Installation

Using npm: `npm install puppeteer`

Using yarn: `yarn add puppeteer`

Using pnpm: `pnpm i puppeteer`


## Basic Setup

```javascript
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch({ headless: "new" });

  // Your code here

  await browser.close();
})();

```
## Navigating and Interacting

### Opening a webpage:

```javascript
await page.goto('https://www.example.com');

```

### Clicking on an element:

```javascript
await page.click('button#myButton');
```


### Filling an input field:

```javascript
await page.type('input#myInput', 'Hello, World!');
```


### Taking a screenshot:

```javascript
  await page.screenshot({ path: 'screenshot.png', fullPage: true });
  //delete fullPage or make it false if you dont want the screenshot to be full page
```

## Waiting for Actions and Elements

### Waiting for navigation to complete:

```javascript
await page.waitForNavigation();
```
### Waiting for a specific selector to appear:

```javascript
await page.waitForSelector('div#myElement');
```

### Waiting for a fixed amount of time:

```javascript
await page.waitForTimeout(2000); // 2000 milliseconds
```

## Extracting Information

### Getting the text content of an element:

```javascript
const text = await page.$eval('p#myParagraph', (element) => element.textContent);
```

### Getting the value of an input field:

```javascript
const value = await page.$eval('input#myInput', (element) => element.value);
```
### Extracting data from multiple elements:

```javascript
const elements = await page.$$eval('ul li', (elements) => elements.map((el) => el.textContent));
```
## Handling Dialogs and Alerts

### Accepting an alert dialog:

```javascript
page.on('dialog', async (dialog) => {
  console.log(dialog.message());
  await dialog.accept();
});

```
## Emulating Devices and Network Conditions

### Emulating a specific device:

```javascript
const iPhone = puppeteer.devices['iPhone X'];
await page.emulate(iPhone);
```
### Emulating network conditions:

```javascript
const client = await page.target().createCDPSession();
await client.send('Network.enable');
await client.send('Network.emulateNetworkConditions', {
  offline: false,
  downloadThroughput: 2 * 1024 * 1024,
  uploadThroughput: 1 * 1024 * 1024,
  latency: 20,
});
```
## Handling Errors and Debugging

### Catching errors and handling exceptions:

```javascript
try {
  // Your code here
} catch (error) {
  console.error('An error occurred:', error);
}
```
### Enabling Puppeteer debugging information:

```javascript
process.env['DEBUG'] = 'puppeteer:*';
```

Remember, this cheat sheet provides a basic overview of common Puppeteer tasks. For more detailed information and advanced usage, I recommend referring to the official [Puppeteer documentation](https://pptr.dev/).


