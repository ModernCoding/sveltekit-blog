<script type="text/javascript" context="module">

  export const load = async ({ fetch, params }) => {

    const post = await (async url =>
            
        await (async promise =>
          await promise.json ()
        ) (await fetch (url))

      ) (`https://jsonplaceholder.typicode.com/posts/${ params.id }`) 


    return {
      props: { post }
    }

  }

</script>


<script type="text/javascript">
  export let post = {}
</script>


<h1>#{ post.id }: { post.title }</h1>
<p>{ post.body }</p>
<a sveltekit:prefetch href="/">All posts</a>