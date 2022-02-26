<script type="text/javascript" context="module">

  export const load = async ({ fetch }) => {

    return {
      
      props: {

        posts: await (async promise =>
            await promise.json ()
          ) (await fetch ('https://jsonplaceholder.typicode.com/posts'))

      }

    }

  }

</script>


<script type="text/javascript">
  export let posts
</script>


<h1>Posts</h1>

{#each posts as post}

  <article>
    <h2>#{ post.id }: { post.title }</h2>
    <p>{ post.body }</p>
  </article>

{/each}
