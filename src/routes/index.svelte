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

  export let searchTerm = ""
  export let posts

  let currentPage = 1
  const pageSize = 4

  $: searchPosts = posts.filter (p => p.title.includes (searchTerm))
    
  $: paginatedItems
      = paginate ({ items: searchPosts, pageSize, currentPage })

</script>


<h1>Posts</h1>

<input type="text" placeholder="search..." bind:value={ searchTerm }>

{ #each paginatedItems as post }

  <a sveltekit:prefetch href={`/blog/${ post.id }`}>

    <article>
      <h2>#{ post.id }: { post.title }</h2>
      <p>{ post.body }</p>
    </article>

  </a>

{ /each }


<LightPaginationNav
  totalItems="{searchPosts.length}"
  pageSize="{pageSize}"
  currentPage="{currentPage}"
  limit="{1}"
  showStepOptions="{true}"
  on:setPage="{(e) => currentPage = e.detail.page}"
/>