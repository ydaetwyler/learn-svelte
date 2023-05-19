<script>
  // Nested import
  import Nested from './Nested.svelte'

  // Br import
  import Br from './Br.svelte'

  // Button
  let user = { loggedIn: false }

  const toggle = () => user.loggedIn = !user.loggedIn

  // cick count
  let count = 0
  $: doubled = count * 2

  $: if (count >= 10) {
    alert('count is dangerously high!')
    count = 9
  }

  const incrementCount = () => count++

  // numbers
  let numbers = [1, 2, 3, 4]

  const addNumber = () => numbers = [...numbers, numbers.length + 1]

  $: sum = numbers.reduce((t, n) => t + n, 0)
</script>

<!-- click count -->
<button on:click={incrementCount}>
  Clicked {count} {count === 1 ? 'time' : 'times'}  
</button>

<p>{count} doubled ist {doubled}</p>

<Br />

<!-- numbers -->
<p>{numbers.join(' + ')} = {sum}</p>

<button on:click={addNumber}>
  Add a number
</button>

<Br />

<!-- Nested -->
<Nested answer={43}/>
<Nested/>

<Br />

<!-- Button -->
{#if user.loggedIn}
  <button on:click={toggle}>
    Log out
  </button>
{/if}

{#if !user.loggedIn}
  <button on:click={toggle}>
    Log in
  </button>
{/if}
