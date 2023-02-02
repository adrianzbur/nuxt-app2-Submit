<template>
    <main>
      <h1>Zoznam ľudí</h1>
      <section class="list">
        <section v-for="person of persons" v-bind:key="person"
        v-bind:class="{'card-container':true,'card':true,'adult': calculateAge(person)>=18,'elders':calculateAge(person)>=70,'youngsters':calculateAge(person)<=10}"><!--v tomto prípade clase priradíme objekt, ktorého vlastnosti predstavujú jednotlivé triedy a ich hodnoti predstavujú bool vyjadrujúci, kedy sa má daná trieda pridať danému elemntu-->
        <!--alebo takto tu to poriešime ternárnym operátorom...
        <section v-for="person of persons" v-bind:key="person" 
        v-bind:class="person.age>=18 ? 'adult card-container card' : 'card-container card'">
        -->
        <personCard @editWasClicked ="editPerson" @removeWasClicked = "removePerson" v-bind:person = "person"></personCard>
        </section>
    </section>
    <div v-on:click ="deleteAll()" class="btn" v-if="bool == true">Delete all</div>
	<div v-on:click ="submit()" class="btn" v-if="bool == true">Submit</div>
    <input v-model="name" placeholder="name">
    <div>{{name}}</div>
    </main>
</template>

<script setup>

function calculateAge({birthday}){
    let currentDate = new Date();
    let currentYear = currentDate.getFullYear();
    
    return currentYear - birthday;
}


let initialPersons = [
        {
            fname: "Magdalena",
            lname: "Mikulova",
            day: 11,
            month: 1,
            birthday: 1877,

        },
        {
            fname: "Sofia",
            lname: "Zlatkovicova",
            day: 31,
            month: 12,
            birthday: 2015,
            
        },
        {
            fname: "Hugo",
            lname: "Trubic",
            birthday: 2008,
            day: 6,
            month: 4,
            
        },
        {
            fname: "Miki",
            lname: "Spis",
            day: 18,
            month: 10,
            birthday: 2012,
        
        },
        {
            fname: "Andrea",
            lname: "Veresova",
            day: 8,
            month: 9,
            birthday: 1888,
            
        },
        {
            fname: "Nora",
            lname: "Mojsejova",
            day: 12,
            month: 7,
            birthday: 1966,
         
        },
    ]

    let persons = ref(initialPersons)
	let name = ref("")
    let bool = ref(true)
	let card
	
    const editPerson = (personShouldBeEdited) => {
        persons.value.forEach((item) => {
            if(item == personShouldBeEdited){
                name.value=item.fname

                card = item
                console.log(card)
            }
        })

    }


    const submit = () => {
        persons.value.forEach((item) => {
            if(item == card){
                item.fname=name.value
				name.value = ""
            }
        })
    }


    const deleteAll = () => {
        persons.value = [];
        console.log("Ludia boli vymazany dakujem")
        bool = false;
        name.value= ""
    }

    const removePerson = (personShouldBeRemoved) => {
        persons.value = persons.value.filter(item=>item!= personShouldBeRemoved)

    }


</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;500;600;700&display=swap');
    body {
        font-size: 10px;    
        font-family: 'Oswald', sans-serif;
        padding: 1rem;
        background: linear-gradient(rgba(248, 225, 225, 0.493),rgb(0, 204, 255));
        background-attachment: fixed;
    }
    main {
        display: flex;
        flex-direction: column;
        gap: .75rem;
    }
    .list {
        display: flex;
        gap: 20px;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: stretch;
        font-size: 1.2rem;
    }
    .card-container {
        flex-grow: 1;
    }
</style>