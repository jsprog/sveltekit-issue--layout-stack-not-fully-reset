<script context="module">
    console.log('%c routes/__layout.svelte  -  module ', 'color: blue; font-weight: bold;')
</script>

<script>
    console.log('%c routes/__layout.svelte  -  instance ', 'color: rgba(0,0,255,0.6); font-weight: bold;')
    import Component from '$lib/Component.svelte'
    import mod from '$lib/module'

    // console.log(Component, mod)
</script>

<h2 style="color: blue;">routes/__layout.svelte</h2>
<slot></slot>
