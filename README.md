# Layout Stack not Fully Reset for src/routes/__layout.svelte

### Describe the bug:

According to the official sveltekit documentation, adding __layout.reset.svelte inside a nested folder should reset layout stack and prevent inheriting from upper level layouts. Unfortunately, the browser is receiving some logs from the **module context** of `__src/routes/__layout.svelte`. ssr logs are clean and not affected.

### Reproduction:
- sveltekit skeleton project: npm init svelte@next layout-stack-not-fully-reset
- add some files: `src/routes/__layout.svelte`, `src/routes/login/__layout.reset.svelte`, and `src/routes/login/index.svelte` containing the following:
```svelte
<!-- src/routes/__layout.svelte -->
<script context="module">
    console.log('%c routes/__layout.svelte  -  module ', 'color: blue; font-weight: bold;')
</script>

<script>
    console.log('%c routes/__layout.svelte  -  instance ', 'color: rgba(0,0,255,0.6); font-weight: bold;')
</script>

<h2 style="color: blue;">routes/__layout.svelte</h2>
<slot></slot>
```

```svelte
<!-- src/routes/login/__layout.reset.svelte> -->
<script context="module">
    console.log('%c routes/login/__layout.reset.svelte  -  module ', 'color: darkgreen; font-weight: bold;')
</script>

<script>
    console.log('%c routes/login/__layout.reset.svelte  -  instance ', 'color: rgba(0,100,0, 0.6); font-weight: bold;')
</script>

<h2 style="color: darkgreen;">routes/login/__layout.reset.svelte</h2>
<slot></slot>
```

```svelte
<!-- src/routes/login/index.svelte -->
<p style="color: darkgreen;">routes/login/index.svelte</p>
{#if false}<slot />{/if}
```

- replace the content of the main index.svelte file with this:
```svelte
<!-- src/index.svelte -->
<p style="color: blue;">routes/index.svelte</p>
{#if false}<slot />{/if}
```

### System Info:
System:
    OS: Linux 4.19 LMDE 4 (debbie) 4 (debbie)
    CPU: (4) x64 Intel(R) Core(TM) i5-3570K CPU @ 3.40GHz
    Memory: 10.01 GB / 15.56 GB
    Container: Yes
    Shell: 5.0.3 - /bin/bash
  Binaries:
    Node: 14.17.1 -
    npm: 6.14.13 -
  Browsers:
    Chrome: 92.0.4515.131
    Firefox: 68.8.0esr


### Additional Information:
- ssr logs are not affected by this.
- other nested layout files are not affected by this, and their children `__layout.reset.svelte` are fully resetting them.
