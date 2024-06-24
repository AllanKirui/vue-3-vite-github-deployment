<script setup>
const copyCode = (codeId, event) => {
  const copyBtn = event.target
  copyBtn.blur()

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
        <li>
          <a href="#fixing-404-error">
            Fixing the 404 Error Displayed by GitHub Pages When Reloading or Entering Direct URLs
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
        <div class="pre-wrapper">
          <pre>
  <code id="code1">
  <span class="terminal-command">npm create <span class="package">vue@latest</span></span>
  </code>
</pre>
          <button @click="($event) => copyCode('code1', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 2 -->
      <div class="step">
        <h3>2. Install Vue Router</h3>
        <p>If you chose to install Vue Router in Step 1 above, skip this step.</p>
        <div class="pre-wrapper">
          <pre>
   <code id="code2">
   <span class="terminal-command">npm install <span class="package">vue-router</span></span>
   </code>
</pre>
          <button @click="($event) => copyCode('code2', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 3 -->
      <div class="step">
        <h3>3. Configure Vue Router</h3>
        <p>
          Create a <code>router</code> directory inside the <code>src</code> folder and add an
          <code>index.js</code> file.
        </p>
        <div class="pre-wrapper">
          <pre>
   <code id="code3">
   <span class="terminal-command">mkdir</span> <span class="flag">src/router</span>
   <span class="terminal-command">touch</span> <span class="flag">src/router/index.js</span>
   </code>
</pre>
          <button @click="($event) => copyCode('code3', $event)">Copy Code</button>
        </div>

        <p>In <code>src/router/index.js</code>, set up your routes:</p>
        <div class="pre-wrapper">
          <pre>
   <code id="code4">
   <span class="keyword">import</span> <span class="method"></span><span class="method">{ createRouter, createWebHistory }</span> <span class="keyword">from</span> <span class="string">'<span class="package">vue-router</span>'</span>;
   <span class="keyword">import</span> <span class="method">Home</span> <span class="keyword">from</span> <span class="string">'../views/Home.vue'</span>;
   <span class="keyword">import</span> <span class="method">About</span> <span class="keyword">from</span> <span class="string">'../views/About.vue'</span>;
   
   <span class="keyword">const</span> routes = [
     { <span class="keyword">path</span>: <span class="string">'/'</span>, <span class="keyword">component</span>: Home },
     { <span class="keyword">path</span>: <span class="string">'/about'</span>, <span class="keyword">component</span>: About },
   ];
   
   <span class="keyword">const</span> router = createRouter({
     <span class="keyword">history</span>: createWebHistory(<span class="keyword">import</span>.meta.env.BASE_URL),
     <span class="keyword">routes</span>,
   });
   
   <span class="keyword">export</span> <span class="package">default</span> router;
   </code>
</pre>
          <button @click="($event) => copyCode('code4', $event)">Copy Code</button>
        </div>

        <p>Create the <code>views</code> directory and add your components:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code5">
  <span class="terminal-command">mkdir</span> <span class="flag">src/views</span>
  <span class="terminal-command">touch</span> <span class="flag">src/views/Home.vue src/views/About.vue</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code5', $event)">Copy Code</button>
        </div>

        <p>Example <code>Home.vue</code>:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code6">
  <span class="html-tag">&lt;template&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;h1&gt;</span>Home<span class="html-tag">&lt;/h1&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
  <span class="html-tag">&lt;/template&gt;</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code6', $event)">Copy Code</button>
        </div>

        <p>Example <code>About.vue</code>:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code7">
  <span class="html-tag">&lt;template&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;h1&gt;</span>About<span class="html-tag">&lt;/h1&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
  <span class="html-tag">&lt;/template&gt;</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code7', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 4 -->
      <div class="step">
        <h3>4. Use the router in your app</h3>
        <p>In <code>src/main.js</code>, import and use the router:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code8">
  <span class="keyword">import</span> <span class="method">{ createApp }</span> <span class="keyword">from</span> <span class="string">'<span class="package">vue</span>'</span>;
  <span class="keyword">import</span> <span class="method">App</span> <span class="keyword">from</span> <span class="string">'./App.vue'</span>;
  <span class="keyword">import</span> <span class="method">router</span> <span class="keyword">from</span> <span class="string">'./router'</span>;

  <span class="keyword">const</span> app = createApp(App);

  app.use(router);

  app.mount(<span class="string">'#app'</span>);
  </code>
</pre>
          <button @click="($event) => copyCode('code8', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 5 -->
      <div class="step">
        <h3>5. Update the <code>App.vue</code> to include router-view</h3>
        <div class="pre-wrapper">
          <pre>
  <code id="code9">
  <span class="html-tag">&lt;template&gt;</span>
    <span class="html-tag">&lt;header&gt;</span>
      <span class="html-tag">&lt;nav&gt;</span>
        <span class="html-tag">&lt;router-link</span> <span class="property">to</span>=<span class="string">"/"</span><span class="html-tag">&gt;</span>Home <span class="html-tag">&lt;/router-link&gt;</span>
        <span class="html-tag">&lt;router-link</span> <span class="property">to</span>=<span class="string">"/about"</span><span class="html-tag">&gt;</span>About <span class="html-tag">&lt;/router-link&gt;</span>
      <span class="html-tag">&lt;/nav&gt;</span>
    <span class="html-tag">&lt;/header&gt;</span>

    <span class="html-tag">&lt;router-view /&gt;</span>
  <span class="html-tag">&lt;/template&gt;</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code9', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 6 -->
      <div class="step">
        <h3>6. Test your app locally</h3>
        <div class="pre-wrapper">
          <pre>
  <code id="code10">
  <span class="terminal-command">npm run dev</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code10', $event)">Copy Code</button>
          <p>Open the provided local server address in your browser to see your app in action.</p>
        </div>
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
        <div class="pre-wrapper">
          <pre>
  <code id="code11">
  <span class="keyword">import</span> <span class="method">{ defineConfig }</span> <span class="keyword">from</span> <span class="string">'<span class="package">vite</span>'</span>;
  <span class="keyword">import</span> <span class="method">vue</span> <span class="keyword">from</span> <span class="string">'<span class="package">@vitejs/plugin-vue'</span></span>;

  <span class="keyword">export</span> <span class="package">default</span> defineConfig({
    <span class="keyword">base</span>: <span class="string">'/REPOSITORY/'</span>,
    <span class="keyword">plugins</span>: [<span class="method">vue()</span>],
  });
  </code>
</pre>
          <button @click="($event) => copyCode('code11', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 8 -->
      <div class="step">
        <h3>8. Deploy to GitHub Pages</h3>
        <p>Install <code>gh-pages</code>:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code12">
  <span class="terminal-command">npm install <span class="package">gh-pages</span> <span class="flag">--save-dev</span></span>
  </code>
</pre>
          <button @click="($event) => copyCode('code12', $event)">Copy Code</button>
        </div>

        <p>Add deploy scripts to your <code>package.json</code>:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code13">
  <span class="string">"scripts"</span>: {
    <span class="string">"build"</span>: <span class="string">"vite build"</span>,
    <span class="string">"predeploy"</span>: <span class="string">"npm run build"</span>,
    <span class="string">"deploy"</span>: <span class="string">"gh-pages -d dist</span>"
  }
  </code>
</pre>
          <button @click="($event) => copyCode('code13', $event)">Copy Code</button>
        </div>

        <p>Commit your changes:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code14">
  <span class="git-command">git add .</span>
  <span class="git-command">git commit</span> <span class="flag">-m</span> <span class="string">"Set up Vue 3 Vite app with dynamic routing and deploy to GitHub"</span>
  <span class="git-command">git push</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code14', $event)">Copy Code</button>
        </div>

        <p>Deploy your app:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code15">
  <span class="terminal-command">npm run deploy</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code15', $event)">Copy Code</button>
        </div>
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
        <div class="pre-wrapper">
          <pre>
  <code id="code16">
  <span class="terminal-command">npm run dev</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code16', $event)">Copy Code</button>
          <p>
            Open the provided local server address in your browser to see your updated app in
            action.
          </p>
        </div>
      </div>

      <!-- Step 3 -->
      <div class="step">
        <h3>3. Commit your changes</h3>
        <p>Once you're satisfied with your changes, commit them to your local Git repository:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code17">
  <span class="git-command">git add .</span>
  <span class="git-command">git commit</span> <span class="flag">-m</span> <span class="string">"Describe your changes"</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code17', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 4 -->
      <div class="step">
        <h3>4. Push your changes to GitHub</h3>
        <p>Push your committed changes to your remote repository on GitHub:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code18">
  <span class="git-command">git push</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code18', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 5 -->
      <div class="step">
        <h3>5. Deploy the updated app to GitHub Pages</h3>
        <p>Run the deploy script to build your project and update the GitHub Pages deployment:</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code19">
  <span class="terminal-command">npm run deploy</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code19', $event)">Copy Code</button>
        </div>
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

    <!-- Fixing 404 Errors -->
    <section id="fixing-404-error" class="guide-3">
      <h2 class="guide-title">
        Fixing the 404 Error Displayed by GitHub Pages When Reloading or Entering Direct URLs
      </h2>

      <!-- Step 1 -->
      <div class="step">
        <h3>1. Build your app</h3>
        <p>
          After completing your development work, build your Vue 3 Vite app to generate the
          production-ready files.
        </p>
        <div class="pre-wrapper">
          <pre>
  <code id="code20">
  <span class="terminal-command">npm run build</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code20', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 2 -->
      <div class="step">
        <h3>2. Copy 'index.html' to '404.html'</h3>
        <p>
          Copy the contents of the 'index.html' file generated in the 'dist' folder into a new
          '404.html' file.
        </p>
        <div class="pre-wrapper">
          <pre>
  <code id="code21">
  <span class="terminal-command">cp</span> <span class="flag">dist/index.html public/404.html</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code21', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 3 -->
      <div class="step">
        <h3>3. Deploy your app</h3>
        <p>Deploy your app to GitHub Pages as usual.</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code22">
  <span class="terminal-command">npm run deploy</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code22', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 4 -->
      <div class="step">
        <h3>4. Update '404.html' when making changes</h3>
        <p>
          Whenever you make changes to your code and rebuild the app, update the '404.html' file
          with the new content from 'dist/index.html'
        </p>
        <div class="pre-wrapper">
          <pre>
  <code id="code23">
  <span class="terminal-command">cp</span> <span class="flag">dist/index.html public/404.html</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code23', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Step 5 -->
      <div class="step">
        <h3>5. Redeploy your updated app</h3>
        <p>After updating the '404.html' file, redeploy your app to GitHub pages.</p>
        <div class="pre-wrapper">
          <pre>
  <code id="code24">
  <span class="terminal-command">npm run deploy</span>
  </code>
</pre>
          <button @click="($event) => copyCode('code24', $event)">Copy Code</button>
        </div>
      </div>

      <!-- Foot Note -->
      <div class="foot-note">
        <p>
          Following these steps ensures that your Vue 3 Vite app deployed on GitHub Pages will
          handle reloads and direct URL access correctly without displaying 404 error pages.
        </p>
      </div>
    </section>

    <p class="foot-note">Coding is Your Superpower ✌</p>
  </main>
</template>
