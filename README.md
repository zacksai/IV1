# Intervene


## Step 1: Set up Git Repository

In your local file system:

1. Create and enter directory for project

    ```
    > mkdir IV1
    > cd IV1
    ```

2. Create Git repo, add README.md
    ```
    > git init
    > echo "# Intervene" >> README.md
    > git add README.md
    > git commit -m "initial commit"
    ```

3. Connect to remote, push updates
    ```
    > git remote add origin [SSH/HTTPS address]
    > git push -u origin main
    ```

## Step 2: Create Docker Container

1. Start docker, run the daemon, and pull in the environment:

    ` docker pull mcr.microsoft.com/playwright:v1.40.0-jammy`

2. Copy Dockerfile.jammy into this directory

    `curl -LJO https://github.com/microsoft/playwright/raw/main/utils/docker/Dockerfile.jammy`


Now, before we run the image for tests, let's add the Playwright folder:

## Step 3: Add Playwright Test Folders

1. Add test file
    ```
    mkdir tests
    touch homepage.test.js

    echo "
    const playwright = require('playwright');

    (async () => {
        const browser = await playwright.chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://intervene.io');

        const title = await page.title();
        console.assert(title === 'Home - Intervene', 'Test failed: Title is ${title}');
        console.log("finished");
        console.log("title is", title);
        await browser.close();
    })();" >> homepage.test.js
    ```

2. Add playwright
`npm install playwright`

3. Run the image 
` docker run -it --rm -v $(pwd)/tests:/tests --ipc=host mcr.microsoft.com/playwright:v1.40.0-jammy /bin/bash`

4. Run the test
```
cd tests
node homepage.test.js
```