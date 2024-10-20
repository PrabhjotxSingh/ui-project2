<script>
    export let closePopup;
  
    let favorites = [
      { title: "Neha Toast", breadType: "Bread", time: 2, heat: "Medium" },
      { title: "Quick Bagel", breadType: "Bagel", time: 3, heat: "High" },
      { title: "Crispy Waffle", breadType: "Waffle", time: 4, heat: "Low" },
    ];
  
    let showAddForm = false; // Controls whether the form is visible or not
  
    let newFavorite = {
      title: "",
      breadType: "",
      time: 0,
      heat: ""
    };
  
    function deleteFavorite(index) {
      favorites = favorites.filter((_, i) => i !== index);
    }
  
    function addFavorite() {
      favorites = [...favorites, newFavorite]; // Add the new favorite to the array
      newFavorite = { title: "", breadType: "", time: 0, heat: "" }; // Reset the form
      showAddForm = false; // Hide the form after adding
    }
  
    function openAddForm() {
      showAddForm = true; // Show the form when the button is clicked
    }
  
    function closeAddForm() {
      showAddForm = false; // Hide the form without adding
    }
  </script>
  
  <div class="popup">
    <h3>Favorites</h3>
    <div class="favorites-list">
      {#each favorites as favorite, i}
        <div class="card">
          <h4>{favorite.title}</h4>
          <p>Bread Type: {favorite.breadType}</p>
          <p>Time: {favorite.time} minutes</p>
          <p>Heat: {favorite.heat}</p>
          <button on:click={() => deleteFavorite(i)}>Delete</button>
        </div>
      {/each}
    </div>
  
    <button on:click={openAddForm}>Add New Favorite</button>
    <button on:click={closePopup}>Close</button>
  
    <!-- Show form if "Add New Favorite" is clicked -->
    {#if showAddForm}
      <div class="form-popup">
        <h4>Add New Favorite</h4>
        <label>Title</label>
        <input type="text" bind:value={newFavorite.title} placeholder="Enter title" />
        
        <label>Bread Type</label>
        <input type="text" bind:value={newFavorite.breadType} placeholder="Enter bread type" />
        
        <label>Time (minutes)</label>
        <input type="number" bind:value={newFavorite.time} min="0" placeholder="Enter time in minutes" />
        
        <label>Heat</label>
        <input type="text" bind:value={newFavorite.heat} placeholder="Enter heat level" />
        
        <button on:click={addFavorite}>Add</button>
        <button on:click={closeAddForm}>Cancel</button>
      </div>
    {/if}
  </div>
  
  <style>
    .popup {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: white;
      padding: 20px;
      border: 2px solid black;
      z-index: 1000;
      width: 300px;
    }
    .favorites-list {
      margin-top: 10px;
    }
    .card {
      border: 1px solid gray;
      padding: 10px;
      margin-bottom: 10px;
    }
    .form-popup {
      margin-top: 20px;
      padding: 10px;
      border: 1px solid black;
      background-color: #f9f9f9;
    }
    label {
      display: block;
      margin: 10px 0 5px 0;
    }
    input {
      width: 100%;
      padding: 5px;
      margin-bottom: 10px;
    }
    button {
      margin-top: 10px;
      padding: 5px 10px;
    }
  </style>
  