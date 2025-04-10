# In this part we will be discussing in details about our frontend project

We use Svelte kit as our frontend framework which is the free and open-source PHP-based web framework for building web applications.

What Is Vite?
You mentioned that your project has vite.config.js—this means your project uses Vite as its build tool.
What does Vite do?
Fast Development Server: Vite serves your Svelte project in development mode super fast.

Hot Module Replacement (HMR): When you save a file, only the changed part reloads in the browser.

Build Optimizations: It bundles and optimizes your app for production.

SvelteKit uses Vite under the hood to improve performance.

Project Structure Overview
The basic SvelteKit project might looks like this as shown below:
````perl
my-sveltekit-app/
│── src/
│   ├── routes/        # Page-based routing (SvelteKit feature)
│   ├── lib/           # Reusable components, stores, utils
│   ├── app.html       # Main HTML template
│   ├── main.js        # Entry point (sometimes not needed in SvelteKit)
│── static/            # Public assets (images, fonts, etc.)
│── svelte.config.js   # SvelteKit configuration
│── vite.config.js     # Vite configuration
│── package.json       # Dependencies & scripts
│── node_modules/      # Installed dependencies

````