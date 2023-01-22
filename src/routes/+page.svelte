<script>
  import { browser } from '$app/environment'
  import { env } from '$env/dynamic/public'

  //@todo: change this, so is not public?
  const key = env.PUBLIC_API_KEY

  /**
   * 
   * @param {string} req
   */
  const baseRequest = (req) => `https://4.dbt.io/api/${req}${req.includes('?') ? '&' : '?'}v=4&key=${key}`

  const bibleId = 'ENGKJV'

  /**
   * 
   * @param {string} id
   * @param {string} book
   * @param {number} chapter
   */
  const fetchChapter = async (id, book, chapter) => await fetch(baseRequest(`bibles/filesets/${id}/${book}/${chapter}?verse_start=1`)).then(x => x.json())

  /**
   * 
   * @param {string} id
   */
  const fetchBible = async (id) => await fetch(baseRequest(`bibles/filesets/${id}`)).then(x => x.json())

    /**
   * 
   * @param {string} lang
   */
   const fetchBiblesList = async (lang) => await fetch(baseRequest(`bibles?language_code=${lang}`)).then(x => x.json())

  $: if (browser) console.log(fetchBible(bibleId))

  //$: if (browser) console.log(fetchChapter(bibleId, 'GEN', 5))
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
