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

  import { paginate, LightPaginationNav } from 'svelte-paginate'

  export let posts

  let currentPage = 1
  let pageSize = 4
  $: paginatedItems = paginate({ items: posts, pageSize, currentPage })

</script>


<h1>Posts</h1>

{ #each paginatedItems as post }

  <a sveltekit:prefetch href={`/blog/${ post.id }`}>

    <article>
      <h2>#{ post.id }: { post.title }</h2>
      <p>{ post.body }</p>
    </article>

  </a>

{ /each }


<LightPaginationNav
  totalItems="{posts.length}"
  pageSize="{pageSize}"
  currentPage="{currentPage}"
  limit="{1}"
  showStepOptions="{true}"
  on:setPage="{(e) => currentPage = e.detail.page}"
/>