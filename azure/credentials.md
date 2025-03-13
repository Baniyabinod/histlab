New subscription "Lab- Binod Baniya (FOF)" was created by Rolf Anderson to me and then using that I am able to create the new resource group in the Azure. I have created the a resource group such as "HistLabProject" and that used to create many services such as App service and then Azure Database.

# Azure Database for MySql flexible server

credentials used:
````bash
Binod1
pw: @@rhdtest1
````

Once the Azure database for MySql was created inside the Azure , opened it and went into connect section.Following commands were executed to dump the database into Azure.

conncetion details:
````bash
hostname=rhdtestprod.mysql.database.azure.com
port=3306
username=Binod1
password={your-password}
ssl-mode=require
````



Steps to connect to the database and then dump our sql database into the Azure

1. mysql -h rhdtestprod.mysql.database.azure.com -P 3306 -u Binod1 -p
Enter my password: @@rhdtest1

2. After the connection is successful, If we do `show database`, we can see rhd prod as the new database that we create in Azure.
database name: rhdprod

3. Then before dumping our database, we used the command `use rhdprod`

4. Then , I dumped my database from the computer using this command where I directly source it through my local machine and it took quite some time to dump all the databases.



# rhd-backend in Azure

Created the backend app service in Azure to host our laravel application. The new resource group was created automatically named as rhdtestprod with the location in Norway East.Linux operating system was used and by giving the name(rhd-backend), where the publising model was selected as the "Code"  and runtime stack was "php /8.2"

Once this was created, for the deployment, went into the deployment section where,the option to connect the github was available.I select my github account,sigin in  and then, selected the repo(https://github.com/Baniyabinod/UiT-history-project-backend).

The next step would be to save the configurations. After that the deployment is carried out automatically and then on the overview page, got the message that deployment was successful.


Then for the testing purpose, use this default domain name(rhd-backend-eufmcjg8c9hhekdd.norwayeast-01.azurewebsites.net) from the overview page into my svelte project inside `vite.config.js` which shows that the page was hosted without database for now.

````bash
import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';

export default defineConfig({
    plugins: [sveltekit()],
    server: {
        proxy: {
          '/api': {
            target: 'rhd-backend-eufmcjg8c9hhekdd.norwayeast-01.azurewebsites.net',
            //rhd-backend-eufmcjg8c9hhekdd.norwayeast-01.azurewebsites.net
            //http://127.0.0.1:8000/
            changeOrigin: true,
            secure: false,
            rewrite: (path) => path.replace(/^\/api/, ''),
          },
        },
      },
});
````


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







/history : page has the perfect lenght of the text 
problems wtih less importance.
1. my mac the home page is of perfect size but for the larger screen in my office the home page looks wit lots of space on the box.
2. width of the container in the about us page looks nice in mac but it doesnot look good in large screen.
3. width of the container in the contact us page looks nice in mac but it is not good in large screen
4. 
