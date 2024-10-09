<script>
  import Modal from "./lib/Modal.svelte";
  import AddPersonForm from "./lib/AddPersonForm.svelte";

  let showModal = false;

  const toggleModal = () => {
    showModal = !showModal;
  };

  let people = [
    { name: "yoshi", beltColor: "black", age: 25, skills: ["running"], id: 1 },
    { name: "mario", beltColor: "orange", age: 15, skills: ["sneaking"], id: 2 },
    { name: "luigi", beltColor: "brown", age: 21, skills: ["running", "fighting"], id: 3 },
  ];

  const handleClick = (id) => {
    people = people.filter((person) => person.id != id);
    console.log(id);
  };

  const addPerson = (e) => {
    const person = e.detail;
    people = [person, ...people];
    showModal = false;
  };
</script>

<Modal {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
  <button on:click={toggleModal} style="background: lightcoral;"
    >Open Modal</button
  >
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColor === "black"}
        <p><strong>MASTER NINJA</strong></p>
      {/if}
      <p>{person.age} years old, {person.beltColor} belt.</p>
      {#if person.skills}
        <h5>Skills: {person.skills.join(", ")}</h5>
      {/if}
      <button on:click={() => handleClick(person.id)}>delete </button>
    </div>
  {:else}
    <p>There are no people to show</p>
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
