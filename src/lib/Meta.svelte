<script>
    export let title = "Chooser — Smart choices, simplified.";
    export let siteName = "Chooser Platform";
    export let description = "The ultimate decision companion for students. Find where to eat based on your budget, mood, and vibe.";
    export let url = "/";
    export let keywords = "Chooser, students, food, budget, restaurants, recommendations";
    export let author = "Chooser Team";
   </script>
   
   <svelte:head>
    <title>{title}</title>
    <meta name="description" content={description} />
    <meta name="author" content={author} />
    <meta name="news_keywords" content={keywords} />
   
    <meta property="og:title" content={title} />
    <meta property="og:site_name" content={siteName} />
    <meta property="og:url" content={url} />
    <meta property="og:description" content={description} />
    <meta property="og:type" content="article" />
    <meta property="og:locale" content="en_US" />
   
    <meta property="og:image" content="{url}/images/site_image.svg" />
    <meta property="og:image:type" content="image/jpeg" />
    <meta property="og:image:width" content="1200" />
    <meta property="og:image:height" content="600" />
   
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:site" content={url} />
    <meta name="twitter:title" content={title} />
    <meta name="twitter:description" content={description} />
    <meta name="twitter:image:src" content="{url}/images/site_image.svg" />
   
    <meta name="robots" content="max-image-preview:large" />
   
    <link rel="canonical" href="{url}/" />
   </svelte:head>