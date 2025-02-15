---
title: Playwright
menu:
  notes:
    name: Playwright
    identifier: notes-pw
    weight: 30
    # Pluralsight Course: Playwright in Node.js Fundamentals
---

{{< note title="Info" >}}
Pluralsight Course: Playwright in Node.js Fundamentals
{{< /note >}}

{{< note title="Page locator" >}}

[https://playwright.dev/docs/locators](https://playwright.dev/docs/locators)

#### page.getByLabel()

get by element by the text of `<label>` tag (of an `<input>` tag)


```javascript
const firstName = page.getByLabel('First name');
await firstName.fill('Anh');
await firstName.clear();

// chaining
await page.getByLabel('First name').fill('Tanaka');
```

#### page.getByRole()

```javascript
await page.getByRole('button', {name: 'Register', exact: true }).click(); 
```

exact: match the name exactly (case sensitive)

#### page.getByText()

```javascript
const message = page.getByText('some message text', {exact: true});
await expect(message).toBeVisible();
```

```javascript
page.getByPlaceHolder()

page.getByAltText()

page.getByTitle()

page.getByTestId()
```

#### page.locator()

Use ccs selector

```javascript
await page.locator('.needs-validation label[for="firstname"]').fill(Anh);
```

Or use xpath

```javascript
await page.locator('//form//button[2').click();
// -> select the 2nd button in the form
```
{{< /note >}}

{{< note title="Filter functions" >}}

Example: get a specific row from a table

```javascript
const rows = page.getByRole('row'); // get all rows
console.log(await rows.count());

const row = page.getByRole('row').filter({hasText: 'Competition'});
// -> filter the row that has the text
console.log(await row.textContent());
```

Get a cell from a table

```javascript
const row = page.getByRole('row')
  .filter({hasText: 'Competition'})
  .getByRole('cell')
  .nth(1); // get the 2nd cell
```
{{< /note >}}

{{< note title="Multiple matches" >}}

```javascript
const buttons = page.getByRole('button');
await buttons.first().textContent();
await buttons.last().textContent();
await buttons.nth(1).textContent();
```

count or loop

```javascript
const buttons = page.getByRole('button');
await expect(buttons).toHaveCount(3);

for (const button of await buttons.all()) {
  console.log(`${await button.textContent()});
}
```

→ buttons.all() converts a locator to an array of its child locators.

```javascript
await page.check('#id');

await page.fill('#id', ‘some text’);
```

{{< /note >}}

{{< note title="Frame locator" >}}

* [https://playwright.dev/docs/api/class-framelocator](https://playwright.dev/docs/api/class-framelocator)
* [https://playwright.dev/docs/frames](https://playwright.dev/docs/frames)

```javascript
const frame = await page.frameLocator('$bar');

await button = frame.getByRole('button');
```

{{< /note >}}

{{< note title="Navigate" >}}
Can goto, go forward, go back, refresh

```javascript
await page.goto('/');
await page.goBack();
await page.goForward();
await page.reload();
```

Options:

```javascript
await page.goto('/', {waitUntil: 'load', timeout: 100});
```

- load: default, all are loaded
- domcontentloaded: HMTL is loaded but scripts, images, stylesheets

`timeout` can be used to test the speed of the page. Set default timeout for all tests in a file:

```javascript
test.use({ navigationTimeout: 8000 });
```

{{< /note >}}

{{< note title="Filling" >}}

Note about datetime value:

- In the browser, the display is based on the local of the browser
- But in the test, we must fill in the field with international format: **yyyy-mm-dd**

```javascript
await page.getByLabel('Date of birth').fill('10-10-2023'); // NG (malformed value)
await page.getByLabel('Date of birth').fill('2023-10-10'); // OK
```

**.fill()**
* Clear the input 
* Sets the input value 
* Very fast 

**.type()**
* Does NOT clear the input
* Sends “keydown-keyup” keyboard events for every character
* Can revoke via: `locator.type()` or `page.keyboard.type()` if we don’t have a locator 

{{< /note >}}

{{< note title="Clicking" >}}

Click many times

```javascript
await btn.click();
await btn.click({ clickCount: 5 });
await btn.click({ button: 'right' });
await btn.click({ modifiers: 'Control' }); // Control + click
```

Double click

```javascript
await btn.dbClick();
```

{{< /note >}}

{{< note title="Checking" >}}

For checkboxes and radio buttons

```javascript
await checkbox.check()
```

<br>
{{< alert type="info" >}}
To very a text area containing some text, use `toHaveValue()`, not `toContainText()`
{{< /alert >}}


{{< /note >}}

{{< note title="Selecting" >}}

For `<select>` tag with `<option>` inside

```javascript
locator.selectOption('red'); // select by a value
locator.selectOption({ label: "Blue" }); 
// ↑　Select by the text inside <option> tag
```

{{< /note >}}

{{< note title="Others" >}}

```javascript
await locator.hover();
await locator.dragTo(anotherLocator);
 
await locator.press('Control+ArrowRight');
await locator.press('Shift+A');
```

[https://playwright.dev/docs/input](https://playwright.dev/docs/input)

{{< /note >}}

{{< note title="Assertion" >}}

```javascript
await expect(page).ToHaveTitle('some title');

await expect(textarea).toBeDisabled();
await expect(textarea).toBeEmpty();
await expect(textarea).toBeEnabled();

const feedback = await page.locator('.error-msg');
await expect(feedback).toHaveCount(3); // there are 3 error messages

for (const message of await feedbac.all()) {
  await expect(message).toBeVisible();
}

await expect(feedback.first()).toContainText('....');

// negate
await expect(page.getByTestId('location')).not.toContainText('Tokyo');

// soft assertion to make the test continue running after an assertion fails 
// INSIDE ONE TEST function
await expect.soft(locator).toContainText('Mumbai');
```

{{< /note >}}

{{< note title="Dialog" >}}

1. Alert → OK button
2. Confirm → OK / Cancel button
3. Prompt → Input + OK / Cancel button

{{< alert type="info">}}
Playwright dismisses dialogs by default.<br>
(It is not like when we run the web in the browser which we have to click some button to dismiss the dialog)
{{< /alert >}}

#### Accept a dialog

→ Click OK

```javascript
page.on('dialog', dialog => dialog.accept());
// accept all dialogs if any
// ↑ var name `dialog` can be any name

await page.goto('/');

const input = page.getByLabel('First name');
await input.fill(name);

await page.getByRole('button', {name: 'Clear'}).click();
await expect(input).toHaveValue('');
// ↑　expect that the input is empty
```

`page.on('dialog')` will apply to all the dialog appearing during the test (in this test function only)

To apply the action to only 1 dialog → `page.once('dialog')`

#### Decline a dialog

The default behavior of Playwright is **dimissing** the dialog

```javascript
page.on('dialog', popup => popup.dimiss());
```

{{< /note >}}

{{< note title="page.on(), page.once()" >}}

#### `page.on('console')`

Capture non-error console messages

```javascript
// Example: check the messages in the console when we click the button
page.on('console', msg => console.log(msg));
// capture the message logged in the console and print it
// must register the lisener before performing the action

await btn.click();
```

#### `page.on('pageerror')`

Capture error console messages

```javascript
page.on('pageerror'), err => {
  console.log(`Found an error: ${error.name}, ${error.message}`);
  expect.soft(error.name).not.toEqual('Error');
}
```

{{< /note >}}

{{< note title="Cookies" >}}

```javascript
await page.context().addCookies([{
  name: 'cookie1',
  value: 'abc',
  url: "https://playwright.dev/"
}]);

console.log(await page.context().cookies());

await page.context().clearCookies();
```

{{< /note >}}

{{< note title="Browser storages" >}}

Local Storage: Persist even after closing the browser

Session Storage: Erased after closing the browser

[https://playwright.dev/docs/api/class-browsercontext](https://playwright.dev/docs/api/class-browsercontext)

```javascript
const storage = await page.context().storageState();

// access cookies via storage
console.log(storage.cookies);

// access local storage
console.log(storage.origins[0].localStorage);
```

{{< /note >}}

{{< note title="Run custom javascript" >}}

Use `page.evaluate()`

```javascript
const storage = await page.evalueate(() => windows.localStorage);
// clear local storage
await page.evaluate(() => windows.localStorage.clear()); 
```

Pass a function in

```javascript
test('example', async({page}) => {
  await page.evaluate(setLocalStorage);
})

function setLocalStorage() {
  localStorage.setItem('key', 'value');
}
```

{{< /note >}}

{{< note title="Download" >}}

Playwright deletes the downloaded files when the page context is closed (after the tests run?)

If a test terminated half-way (such as debugging), Playwright doesn’t delete the downloaded files (we might need to clean it up)

Limitations:

* non-previewable files (such as .zip file) can be downloaded in headed and headless mode
* previewable files can be downloaded in headless mod only

```javascript
const downloadPromise = page.waitForEvent('download');
await page.getByText('Download button').click();

// wait for the file to be downloaded
const download = await downloadPromise;

// save the file to some location (unless it will be deleted after the test)
const suggestedFileName = download.suggestedFilename();
const filePath = '/download' + suggestedFileName();
await download.saveAs(filePath);

// check that the download is successfull
expect(await download.failure()).toBeNull();

// using 'fs' module, we can check the downloaded file in more details
// check the file exists
expect(fs.existsSync(filePath)).toBeTruthy();

// check file size
const fileSizeInBytes = fs.statSync(filePath).size();
expect(fileSizeInBytes).toBeLessThan(20_000);
```

{{< /note >}}

{{< note title="Upload" >}}

Use `setInputFiles()`

```javascript
const uploadInput = page.locator('input[type="file"]');

// upload 1 file
await uploadInput.setInputFiles('download/dummy.pdf');

// upload many files
await uploadInput.setInputFiles(["download/file1.txt", "..."]);

// clear the inpur
await uploadInput.setInputFiles([]);

// after that, click submit button
...
```

{{< /note >}}

{{< note title="Take a screenshot" >}}

```javascript
page.screenshot({
  path: 'screenshots/pic1.png' // if the dir doesn't exist, it will be created
})

page.screenshot({
  fullPage: true,
  mask: await page.getByTestId('location').all(), // mask the content matching this locator
})
```

{{< /note >}}

{{< note title="Test runners > Skip tests" >}}

Skip a group of test

```javascript
test.describe('...', () => {
  test.skip(({ browserName }) => browserName === 'chromium', 'some message' );
  
  test('...', async({page}) => {
    await page.goto('');
    ....
  })
});
```

Skip a test

```javascript
test('...', async({page, browserName}) => {
  test.skip(browserName == 'chromium', '....');
  await page.goto('');
  ...
})
```

{{< /note >}}

{{< note title="Test runners > Setup and teardown" >}}

```javascript
test.beforeEach('...',  async ({page}) => {

});

test.afterEach('...', async ({page}) => {

});

test.beforeAll('...', async() => {

});

test.afterAll('...', async() => {

});
```

test.beforeAll() and test.afterAll() are run by each worker, so it can be run many times if have many workers to run tests (which is the default)


{{< /note >}}

{{< note title="Test runners > Test parameterization" >}}

[https://playwright.dev/docs/test-parameterize](https://playwright.dev/docs/test-parameterize)

Many inputs for a test => put the test function into a loop

```javascript
// array
const people = ['Alice', 'Bob'];

for (const name of people) {
  // make sure the name of the test is not duplicated
  test(`Testing ${name}`, async() => {
    ....
  })
}


// map
const map1 = new Map();
map1.set(2, 20);
map1.set(3, 30);

for (const [key, value] of map1) {
  test(`testing 10x function with ${key} and ${value}`, async() => {
    ...
  })
}

// test provider?
const inputs = [
  ['a', 1, 2],
  ['b', 3, 4],
  ['c', 5, 6]
];

for (const [a, b, c] of inputs) {
  test(`Testing ${a} ${b} ${c}, async() => {
    // ...
  })
}
```

Consider a CSV file for complicated test data


{{< /note >}}

{{< note title="Test runners > Test parallelization" >}}

Playwright runs multiple test files in parallel, and run tests inside a file serially

```javascript
test.describe.configure({mode: 'parallel'}); -> run alls  test in the file in parallel mode
```

Use the global config `fullyParallel` to make all tests run in parallel → recommended because we should write tests that are independent from each other

```javascript
export default defineConfig({
  testDir: '/',
  reporter: 'html',
  fullyParallel: true,
  
  use: {
    ...
  }
});
```

{{< /note >}}

{{< note title="Test runners > Other test. function" >}}

* `test.info()`
* `test.slow()`
* `test.use()`

```javascript
test.use({
  viewPort: {width: 1200, height: 400},
  baseURL: '/',
  locale: 'en-US',
  headless: false,
  javascriptEnabled: false,
  acceptDownloads: true,
  colorScheme: light,
  geolocation: ...
});
```

{{< /note >}}

{{< note title="Configuration" >}}# 

`playwright` fixture (but we almost not need it)

```javascript
test('...', async({playwright}) => {
  const firefoxType = await playwright.firefox.launch();
  const ctx = await firefoxType.newContext();
  const page = await ctx.newPage
})
```

To get a browserType, we can import it.

```javascript
import {test, chromium, firefox} from '@playwright/test';

test('...', async() => {
  // browser level config
  const browser = await chromium.launch({
    headless: false,
    slowMo: 200,
    downloadPath: '/some/path'
  });
  
  // context level config
  const context = await browser.newContext({
    baseURL: '/',
    timezoneId: 'America/New_York',
    locale: 'en-US',
    geolocation: {longitude: 12.123, latitude: 41.2369},
    viewport: {width: 600, heigh: 400},
    javascriptEnabed: false,
    acceptDownloads: false,
  })
  
  // create a page from the context
  const page = await context.newPage();
});
```

Config in a test file: `test.use()`

```javascript
test.use({
  
});

test('...', async()=>{
  ...
});

test.describe('group', () => {
  test.use({
  
  });

  test('...', async()=>{
    ...
  });
});
```

→ the closer configurations will win

{{< /note >}}
