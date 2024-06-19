<script setup>
const copyCode = (codeId) => {
  if (!navigator) {
    alert('Please copy code manually.')
    return
  }

  const codeElement = document.getElementById(codeId)
  const codeText = codeElement.textContent

  navigator.clipboard
    .writeText(codeText)
    .then(() => {
      alert('Code copied to clipboard!')
    })
    .catch((err) => {
      console.error('Could not copy text: ', err)
    })
}
</script>

<template>
  <main>
    <h1 class="title">Vue 3 Vite GitHub Deployment</h1>

    <div class="table-of-contents">
      <p>In this guide:</p>
      <ul>
        <li>
          <a href="#creating-and-deploying">
            Creating and Deploying a Vue 3 Vite App that Uses Dynamic Routing with Vue Router to
            GitHub
          </a>
        </li>
        <li>
          <a href="#updating">
            Updating Your Deployed Vue 3 Vite App on GitHub Pages After Making Changes
          </a>
        </li>
      </ul>
    </div>

    <!-- Initial Deployment -->
    <section id="creating-and-deploying" class="guide-1">
      <h2 class="guide-title">
        Creating and Deploying a Vue 3 Vite App that Uses Dynamic Routing with Vue Router to GitHub
      </h2>

      <!-- Step 1 -->
      <div class="step">
        <h3>1. Set up the Vue 3 Vite project</h3>
        <p>This will prompt you to pick some presets. You could go with the defaults.</p>
        <pre>
  <code id="code1">
  npm create vue@latest
  </code>
           <button @click="copyCode('code1')">Copy Code</button>
         </pre>
      </div>

      <!-- Step 2 -->
      <div class="step">
        <h3>2. Install Vue Router</h3>
        <p>If you chose to install Vue Router in Step 1 above, skip this step.</p>
        <pre>
   <code id="code2">
   npm install vue-router
   </code>
           <button @click="copyCode('code2')">Copy Code</button>
       </pre>
      </div>

      <!-- Step 3 -->
      <div class="step">
        <h3>3. Configure Vue Router</h3>
        <p>
          Create a <code>router</code> directory inside the <code>src</code> folder and add an
          <code>index.js</code> file.
        </p>
        <pre>
   <code id="code3">
   mkdir src/router
   touch src/router/index.js
   </code>
           <button @click="copyCode('code3')">Copy Code</button>
       </pre>

        <p>In <code>src/router/index.js</code>, set up your routes:</p>
        <pre>
   <code id="code4">
   import { createRouter, createWebHistory } from 'vue-router';
   import Home from '../views/Home.vue';
   import About from '../views/About.vue';
   
   const routes = [
     { path: '/', component: Home },
     { path: '/about', component: About },
   ];
   
   const router = createRouter({
     history: createWebHistory(import.meta.env.BASE_URL),
     routes,
   });
   
   export default router;
   </code>
           <button @click="copyCode('code4')">Copy Code</button>
       </pre>

        <p>Create the <code>views</code> directory and add your components:</p>
        <pre>
  <code id="code5">
  mkdir src/views
  touch src/views/Home.vue src/views/About.vue
  </code>
        <button @click="copyCode('code5')">Copy Code</button>
    </pre>

        <p>Example <code>Home.vue</code>:</p>
        <pre>
  <code id="code6">
  &lt;template&gt;
    &lt;div&gt;
      &lt;h1&gt;Home&lt;/h1&gt;
    &lt;/div&gt;
  &lt;/template&gt;
  </code>
        <button @click="copyCode('code6')">Copy Code</button>
    </pre>

        <p>Example <code>About.vue</code>:</p>
        <pre>
  <code id="code7">
  &lt;template&gt;
    &lt;div&gt;
      &lt;h1&gt;About&lt;/h1&gt;
    &lt;/div&gt;
  &lt;/template&gt;
  </code>
        <button @click="copyCode('code7')">Copy Code</button>
    </pre>
      </div>

      <!-- Step 4 -->
      <div class="step">
        <h3>4. Use the router in your app</h3>
        <p>In <code>src/main.js</code>, import and use the router:</p>
        <pre>
  <code id="code8">
  import { createApp } from 'vue';
  import App from './App.vue';
  import router from './router';

  const app = createApp(App);

  app.use(router);

  app.mount('#app');
  </code>
        <button @click="copyCode('code8')">Copy Code</button>
    </pre>
      </div>

      <!-- Step 5 -->
      <div class="step">
        <h3>5. Update the <code>App.vue</code> to include router-view</h3>
        <pre>
  <code id="code9">
  &lt;template&gt;
    &lt;header&gt;
      &lt;nav&gt;
        &lt;router-link to="/"&gt;Home&lt;/router-link&gt;
        &lt;router-link to="/about"&gt;About&lt;/router-link&gt;
      &lt;/nav&gt;
    &lt;/header&gt;

    &lt;router-view /&gt;
  &lt;/template&gt;
  </code>
        <button @click="copyCode('code9')">Copy Code</button>
    </pre>
      </div>

      <!-- Step 6 -->
      <div class="step">
        <h3>6. Test your app locally</h3>
        <pre>
  <code id="code10">
  npm run dev
  </code>
        <button @click="copyCode('code10')">Copy Code</button>
    </pre>
        <p>Open the provided local server address in your browser to see your app in action.</p>
      </div>

      <!-- Step 7 -->
      <div class="step">
        <h3>7. Prepare for deployment</h3>
        <p>
          Update your <code>vite.config.js</code> to set the <code>base</code> path for GitHub
          Pages. Replace <code>REPOSITORY</code> with your GitHub repository name.
        </p>
        <p>
          If you don't have a repository set up for the project, create one and follow the steps
          provided by GitHub for adding a project to the repository.
        </p>
        <pre>
  <code id="code11">
  import { defineConfig } from 'vite';
  import vue from '@vitejs/plugin-vue';

  export default defineConfig({
    base: '/REPOSITORY/',
    plugins: [vue()],
  });
  </code>
        <button @click="copyCode('code11')">Copy Code</button>
    </pre>
      </div>

      <!-- Step 8 -->
      <div class="step">
        <h3>8. Deploy to GitHub Pages</h3>
        <p>Install <code>gh-pages</code>:</p>
        <pre>
  <code id="code12">
  npm install gh-pages --save-dev
  </code>
        <button @click="copyCode('code12')">Copy Code</button>
    </pre>

        <p>Add deploy scripts to your <code>package.json</code>:</p>
        <pre>
  <code id="code13">
  "scripts": {
    "build": "vite build",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
  </code>
        <button @click="copyCode('code13')">Copy Code</button>
    </pre>

        <p>Commit your changes:</p>
        <pre>
  <code id="code14">
  git add .
  git commit -m "Set up Vue 3 Vite app with dynamic routing and deploy to GitHub"
  git push
  </code>
        <button @click="copyCode('code14')">Copy Code</button>
    </pre>

        <p>Deploy your app:</p>
        <pre>
  <code id="code15">
  npm run deploy
  </code>
        <button @click="copyCode('code15')">Copy Code</button>
    </pre>
      </div>

      <!-- Foot Note -->
      <div class="foot-note">
        <p>
          Your Vue 3 Vite app with dynamic routing using Vue Router is now deployed to GitHub Pages.
          You can visit <code>https://USERNAME.github.io/REPOSITORY/</code> to see your live
          application.
        </p>
      </div>
    </section>

    <!-- Updating Your Deployed App -->
    <section id="updating" class="guide-2">
      <h2 class="guide-title">
        Updating Your Deployed Vue 3 Vite App on GitHub Pages After Making Changes
      </h2>

      <!-- Step 1 -->
      <div class="step">
        <h3>1. Make changes to your app</h3>
        <p>Edit your project files as needed to implement your updates.</p>
      </div>

      <!-- Step 2 -->
      <div class="step">
        <h3>2. Test your changes locally</h3>
        <p>Ensure your changes work correctly by running the development server:</p>
        <pre>
  <code id="code16">
  npm run dev
  </code>
  <button @click="copyCode('code16')">Copy Code</button>
       </pre>
        <p>
          Open the provided local server address in your browser to see your updated app in action.
        </p>
      </div>

      <!-- Step 3 -->
      <div class="step">
        <h3>3. Commit your changes</h3>
        <p>Once you're satisfied with your changes, commit them to your local Git repository:</p>
        <pre>
  <code id="code17">
  git add .
  git commit -m "Describe your changes"
  </code>
  <button @click="copyCode('code17')">Copy Code</button>
</pre>
      </div>

      <!-- Step 4 -->
      <div class="step">
        <h3>4. Push your changes to GitHub</h3>
        <p>Push your committed changes to your remote repository on GitHub:</p>
        <pre>
  <code id="code18">
  git push
  </code>
  <button @click="copyCode('code18')">Copy Code</button>
      </pre>
      </div>

      <!-- Step 5 -->
      <div class="step">
        <h3>5. Deploy the updated app to GitHub Pages</h3>
        <p>Run the deploy script to build your project and update the GitHub Pages deployment:</p>
        <pre>
  <code id="code19">
  npm run deploy
  </code>
  <button @click="copyCode('code19')">Copy Code</button>
      </pre>
      </div>

      <!-- Foot Note -->
      <div class="foot-note">
        <p>
          After running these commands, your updated project will be live on GitHub Pages. You can
          visit <code>https://USERNAME.github.io/REPOSITORY/</code> to see the updated version of
          your application.
        </p>

        <p>If you encounter any issues, make sure that:</p>
        <ul>
          <li>
            Your <code>vite.config.js</code> still has the correct <code>base</code> path for your
            repository.
          </li>
          <li>
            You are on the correct branch (usually <code>main</code> or <code>master</code>) when
            you commit and push your changes.
          </li>
        </ul>

        <p>
          By following these steps, you ensure that your updated project is correctly deployed to
          GitHub Pages.
        </p>
      </div>
    </section>

    <p class="foot-note">Coding is Your Superpower ✌</p>
  </main>
</template>
