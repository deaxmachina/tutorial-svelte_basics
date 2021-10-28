<script>
  import Modal from "./Modal.svelte"
  import AddPersonForm from './AddPersonForm.svelte'

  let showModal = false

  const toggleModal = () => {
    showModal = !showModal
  }

  let people = [
    { name: 'yoshi', beltColour: 'black', age: 25, id: 1 },
    { name: 'murio', beltColour: 'orange', age: 45, id: 2 },
    { name: 'luigi', beltColour: 'brown', age: 35, id: 3 },
  ]

  const handleClick = (id) => {
    // delete person from people 
    people = people.filter(person => person.id !== id)
  }

  let num = 40;

  const addPerson = (e) => {
    const newPerson = e.detail // this is how we get the dispatched data 
    people = [newPerson, ...people]
    showModal = false
  }
</script>

<!-- {#if num > 20}
  <p>Greater than 20</p>
{:else if num > 5}
  <p>Greater than 5</p>
{:else}
  <p>Not greater than anything</p>
{/if} -->

<Modal 
  isPromo={true} 
  showModal={showModal}
  on:click={toggleModal}
>
  <AddPersonForm on:addPerson={addPerson} />
  <div slot='title'>
    <h3>Add a new person</h3>
  </div>
</Modal>

<main>
  <button on:click={toggleModal}>Open Modal</button>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColour === 'black'}
      <p><strong>master ninja</strong></p>
      {/if}
      <p>{person.age} years old</p>
      <p>{person.beltColour} belt </p>
      <button 
        on:click={() => handleClick(person.id)}
        >
        delete
      </button>
    </div>
    <br>
  {:else}
    <p>There are no people to show...</p>
  {/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>