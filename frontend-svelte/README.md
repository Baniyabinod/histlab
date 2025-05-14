# Frontend

## Prerequisites

Before you begin, ensure you have the following installed:
````bash
- **Node.js** (v18.x or higher recommended)
- **npm** (v9.x or higher) or **yarn** (v1.22.x or higher)


````

## Getting Started

To learn more about creating the svelte project, visit this link:
[Creating project svelte](https://svelte.dev/docs/kit/creating-a-project)


### 1. Clone the Repository
````bash
git clone https://github.com/Baniyabinod/rhdnew
cd rhdnew

````

2. Install Dependencies
Using npm:

`npm install`

3. Environment Configuration


Edit the .env file to configure:

API base URL (pointing to our backend). In our case, we are using the back end url from the Azure
`https://histlabbackend-fkbxbmhkdbccf0hn.norwayeast-01.azurewebsites.net`

Any other environment-specific variables. We set up other environment like this earlier but we dont need to use it as we have commented this part in the code for email functionality. If needed we can use this in the future.

````bash
VITE_PUBLIC_GMAIL_HOST=smtp.gmail.com
VITE_PUBLIC_GMAIL_USER=baniyabinod348@gmail.com
VITE_PUBLIC_GMAIL_PASS=hvpolqaewwxuldmj

````

4. Change the configuration on the `vite.config.js` file. Right now,in the code the frontend is fetching the data from the Azure resource as shown  here

````bash
export default defineConfig(({ mode }) => ({
  plugins: [sveltekit()],
  server: mode === 'development' ? {
    proxy: {
      '/api': {
        target: 'https://histlabbackend-fkbxbmhkdbccf0hn.norwayeast-01.azurewebsites.net/',
        changeOrigin: true,
        secure: false,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
    },
  } : undefined,
}));

````

However, when we are testing it locally, we have to comment this part in the code and uncomment the part above which  uses the local server as shown here

`target: 'http://127.0.0.1:8000/', `
            

5. Start Development Server
`npm run dev`

The application will be available at:
`http://localhost:8080`