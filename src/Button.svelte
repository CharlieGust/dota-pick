<script>
  function toggle() {
    window.document.body.classList.toggle('dark-mode')
  }
  </script>
  <button on:click={toggle}>
    <slot/>
  </button>
  <style>
    button {
      background-color: #ed2121;
      color: white;
      border: none;
      border-radius: 4px;
      padding: 0.5rem;
      text-transform: uppercase;

    }
    :global(body.dark-mode) button {
      background-color: #ee7f29;
      color: white;
    }
  </style>
