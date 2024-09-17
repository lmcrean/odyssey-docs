# Usage



# 1. **Installation**

It would be advisable to use the [Gitpod IDE](http://gitpod.io) for the installation process, as it is pre-configured with the necessary tools and dependencies, especially around `nvm` and linking to the API.

To get the frontend app up and running locally, follow these steps:

1. **Clone the repository**:
   ```bash
   git clone http://github.com/lmcrean/odyssey_react.git
   ```

2.  Navigate to the `/frontend` directory
   ```bash
   cd frontend
   ```

3. **Install dependencies**:
   install the required dependencies:

   ```bash
   npm install
   ```

4. **Install correct node version**:
   Run the following command to start the React app locally:

   ```bash
   nvm install 16
   ```

5. **Run build**:
   Run the following command to build the React app locally:
   ```bash
   npm run build
   ```

6. **Split the terminal, open the development server**:
   Split the terminal so we can run the API and frontend at the same time

   In terminal 1, run the API.
   ```bash
   python3 manage.py runserver
   ```


   In Terminal 2, go to `/frontend` and open the following command to start the React app locally:
   ```bash
   cd frontend
   npm start
   ```
   This should open in port `8080` or something similar - it will contain the latest changes.


## 1.1. Committing to Production - Note on compiling static files


This command will delete the old `build` and replace it with the new one: 

```bash
npm run build && rm -rf ../staticfiles/build && mv build ../staticfiles/.
```

You will need to re-run this command any time you want to deploy changes to the static files in your project, including the React code. To do this, you need to delete the existing `build` folder and rebuild it.


# 2. Automated Testing Instructions

First, ensure the frontend is opened with:

```bash
cd frontend
```

## 2.1. Jest Testing

Tests are located in the `/__tests__` folder, interspersed throughout the js files in `/frontend` directory. To run the tests, use the following command:

```bash
npm run test
```

## 2.2. Cypress Testing

Tests are located in the `cypress/integration` folder. To run the tests, use the following command:

1. Open a split terminal, run the following command to start the server:

```bash
nvm install 16
npm run build
npm run start
```

2. In the other terminal, run the following command to set up cypress:

```bash
sudo apt-get update
sudo apt-get install -y xvfb libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb
npx cypress install
npx cypress verify
```

3. In the same terminal, run the following command to run the tests:

```bash
npx cypress open
```

or to run a specific test, for example `frontend/cypress/e2e/auth.cy.js` you can write something like this:

```bash
npx cypress run --spec "cypress/e2e/auth.cy.js"
npx cypress run --spec "cypress/e2e/user_journey.cy.js" --headed
```


## 2.3. Playwright Testing

Tests are located in the `playwright` folder. To run the tests, use the following commands:

```bash
npx playwright install --with-deps
npx playwright test
```

if you want to run a specific test, for example `frontend/playwright/auth.test.js` you can write something like this:

```bash
npx playwright test playwright/auth.spec.js
```

# 3. Automated Testing in Backend with python

Tests are located in the `tests` subfolders, each nested in the relevant app folder. To run the tests, use the following command:

```bash
python3 manage.py test
```

Before Starting the tests the following needs to be uncommented in `env.py file`:

```python
os.environ['DEV'] = '1' # Uncomment the following line to enable development mode
```
