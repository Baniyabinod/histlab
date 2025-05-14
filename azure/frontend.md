# Azure fronetent with static web app

## Process of creating the static web app
1. Subscription - Lab - Binod Baniya (FOF)
2. resourece group - HistLab
3. name  - rhd-frontend
4. plan type - free
5. region - global
6. deployment details - github
7. Organization - Baniyabinod
8. repository - UiT-v2
9. branch - main
10. Build Presets - SvelteKit
11. app location - ./
12. api_location - build/server
12. output location - build/static

After all these configurations, we an preview it first and then create it.It will automatically deploy the site and provide us the link for our site which can be found on the overview page.

The link for the test production is given below:



imp:
config in .yml file that hosted the frontend

app_location: "./" # App source code path
api_location: "build/server" # Api source code path - optional
output_location: "build/static" # Built app content directory - optional


# Following configurations are used in the project

````bash
command:npm --version  

output: npm: 10.5.0
command:node --version 

output: node: v21.7.3
command: npm list 

 output:
uit@0.0.1 C:\Users\bba065\work\census\census-frontend\UIT-v2
├── @sveltejs/adapter-auto@3.3.1
├── @sveltejs/adapter-static@3.0.8
├── @sveltejs/package@2.3.7
├── @sveltejs/vite-plugin-svelte@5.0.1
├── @types/nodemailer@6.4.17
├── chart.js@4.4.7
├── leaflet@1.9.4
├── nodemailer@6.10.0
├── publint@0.2.12
├── svelte-check@4.1.1
├── svelte-toasts@1.1.2
├── typescript@5.7.2
└── vite@6.0.3

command: npm list @sveltejs/kit  

output:
uit@0.0.1 C:\Users\bba065\work\census\census-frontend\UIT-v2
├─┬ @sveltejs/adapter-auto@3.3.1
│ └── @sveltejs/kit@2.9.0
└─┬ @sveltejs/adapter-static@3.0.8
  └── @sveltejs/kit@2.9.0 deduped

command:npm list vite  

output:
uit@0.0.1 C:\Users\bba065\work\census\census-frontend\UIT-v2
├─┬ @sveltejs/adapter-auto@3.3.1
│ └─┬ @sveltejs/kit@2.9.0
│   └── vite@6.0.3 deduped
├─┬ @sveltejs/vite-plugin-svelte@5.0.1
│ ├─┬ @sveltejs/vite-plugin-svelte-inspector@4.0.1
│ │ └── vite@6.0.3 deduped
│ ├── vite@6.0.3 deduped
│ └─┬ vitefu@1.0.4
│   └── vite@6.0.3 deduped
└── vite@6.0.3






````


Our frontend project has very few environment variables set in locally as shown below: Since we remove the email option, I have commented it on the code.

````bash
VITE_PUBLIC_GMAIL_HOST=smtp.gmail.com
VITE_PUBLIC_GMAIL_USER=baniyabinod348@gmail.com
VITE_PUBLIC_GMAIL_PASS=hvpolqaewwxuldmj
VITE_BACKEND_URL=https://histlabbackend-fkbxbmhkdbccf0hn.norwayeast-01.azurewebsites.net
````

Since we are using Azure static web app to host our frontend project, we need to specify these environment variables in the workflow .yml file that will bind the varaibles during the production. The .yml file is given below:

````bash
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true
          lfs: false
      - name: Set up Environment Variables
        run: echo "VITE_BACKEND_URL=${{ secrets.VITE_BACKEND_URL }}" >> $GITHUB_ENV
             echo "VITE_PUBLIC_GMAIL_HOST=${{ secrets.VITE_PUBLIC_GMAIL_HOST }}" >> $GITHUB_ENV
             echo "VITE_PUBLIC_GMAIL_USER=${{ secrets.VITE_PUBLIC_GMAIL_USER }}" >> $GITHUB_ENV
             echo "VITE_PUBLIC_GMAIL_PASS=${{ secrets.VITE_PUBLIC_GMAIL_PASS }}" >> $GITHUB_ENV
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_WITTY_MUSHROOM_0743CCA03 }}
          repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
          action: "upload"
          ###### Repository/Build Configurations - These values can be configured to match your app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: "./" # App source code path
          api_location: "build/server" # Api source code path - optional
          output_location: "build/static" # Built app content directory - optional
          ###### End of Repository/Build Configurations ######
        env:
          VITE_BACKEND_URL: ${{ secrets.VITE_BACKEND_URL }}
          VITE_PUBLIC_GMAIL_HOST: ${{ secrets.VITE_PUBLIC_GMAIL_HOST }}
          VITE_PUBLIC_GMAIL_USER: ${{ secrets.VITE_PUBLIC_GMAIL_USER }}
          VITE_PUBLIC_GMAIL_PASS: ${{ secrets.VITE_PUBLIC_GMAIL_PASS }}
        

  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
      - name: Close Pull Request
        id: closepullrequest
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_WITTY_MUSHROOM_0743CCA03 }}
          action: "close"
````

These varaibles alos needs to be inside the github secrets so that it will fetch the value and then link it during the build process in Azure Static Web app.For that, you need to go to settings-secrets and varaibles. Then choose actions and you will see the Secrets maintained inside it.
If this doesnot work, you may also need to configure it in Azure under settings, environment varaibles and add your key value pair there. It is not confirmed at our end but if setting the environment variables only inside github doesnot work then you may have to set it over there aswell.
