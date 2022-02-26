<script type="text/javascript" context="module">

  export const load = async ({ fetch, params }) => {

    const post = await (async url =>
            
        await (async promise =>
          await promise.json ()
        ) (await fetch (url))

      ) (`https://jsonplaceholder.typicode.com/posts/${ params.id }`) 


    const user = await (async url =>
            
        await (async promise =>
          await promise.json ()
        ) (await fetch (url))

      ) (`https://jsonplaceholder.typicode.com/users/${ post.userId }`) 


    return {
      props: { post, user }
    }

  }

</script>


<script type="text/javascript">
  export let post, user
</script>


<h1>#{ post.id }: { post.title }</h1>
<p>{ post.body }</p>
<em>Written by { user.name }</em>
  
<div>
  <a sveltekit:prefetch href="/">All posts</a>
</div>