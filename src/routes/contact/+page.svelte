  <script>
    import { onMount } from "svelte";
  
    const endpoint = "https://rishabh-test-api.vercel.app/api/contact";
    let posts = [];
    let searchTerm = "";
    let filteredPosts = [];
  
    onMount(async function () {
      const response = await fetch(endpoint);
      const data = await response.json();
      posts = data;
    });
  
    function search() {
      if (searchTerm) {
        filteredPosts = posts.filter(post =>
          post.name.toLowerCase().includes(searchTerm.toLowerCase())||
          post.country.toLowerCase().includes(searchTerm.toLowerCase())||
          post.address.toLowerCase().includes(searchTerm.toLowerCase())||
          post.created_at.toLowerCase().includes(searchTerm.toLowerCase())
        );
      } else {
        filteredPosts = [];
      }
    }
  </script>
  
  <main>
    <h1>Contact Page</h1>
  
    <input type="text" bind:value={searchTerm} placeholder="Search Data of User" on:input={search} />
  
    {#if searchTerm && filteredPosts.length === 0}
      <p>No matching data found.</p>
    {:else if filteredPosts.length > 0}
      <ul>
        {#each filteredPosts as post (post.id)}
          <li>
            <strong>{post.name}</strong><br />
            Created On :{post.created_at} <br>
            Phone: {post.phone} <br>
            Address :{post.address} <br>
            Country :{post.country} <br>
          </li>
        {/each}
      </ul>
    {/if}
  </main>
  
 
  
  
  <style>
    main {
      max-width: 800px;
      margin: auto;
      padding: 20px;
      background-color: #f5f5f5;
      border-radius: 8px;
      box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
      margin-top: 10vh;
     
    }
  
    h1 {
      font-size: 24px;
      margin-bottom: 20px;
      color: #333;
      text-align: center;
    }
  
    input[type="text"] {
      padding: 10px;
      width: 90%;
      border: 1px solid #ccc;
      border-radius: 4px;
      margin-bottom: 20px;
      font-size: 16px;
        
    }
  
    input[type="text"]:focus {
      outline: none;
      border-color: #007bff;
      box-shadow: 0px 0px 4px rgba(0, 123, 255, 0.4);
    }
  
    ul {
      list-style: none;
      padding: 0;
    }
  
    li {
      border: 1px solid #ccc;
      border-radius: 4px;
      padding: 10px;
      margin-bottom: 10px;
      background-color: #fff;
    }
  
    li:hover {
      background-color: #f9f9f9;
    }
  
    strong {
      display: block;
      font-size: 18px;
      margin-bottom: 5px;
      color: #333;
    }
  
    p {
      color: #666;
    }
  </style>
  

  