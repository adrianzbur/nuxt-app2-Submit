<script setup>

defineProps(['person'])

function calculateAge({birthday}){
    let currentDate = new Date();
    let currentYear = currentDate.getFullYear();
    
    return currentYear - birthday;
}

</script>

<template>
    <section>
          <article class="info">
            <div class="name">{{person.fname}} {{person.lname}}</div>
            <div class="birthday">{{person.day}}.{{person.month}}. {{person.birthday}} </div>
            <div class="age">{{calculateAge(person)}}<span class="year-title">year</span></div>
          </article>
          <footer class="footer-card">
            <span v-on:click="$emit('editWasClicked', person)" class="btn edit">Edit</span>
            <span v-on:click="$emit('removeWasClicked', person)" class="btn remove">Remove</span>
          </footer>
        </section>
</template>

<style>

.card {
        background: rgba(2, 2, 2, 0.344);
        border: 1px solid #bbb;
        color: #444;
        box-shadow: 0 3px 5px rgba(0,0,0,.2);
        border-top-width: 5px;
        border-top-color: rgb(11, 103, 113);
    }
    .card.adult {
        border-top-color: rgb(0, 255, 0);
    }

    .card.elders{

        border-top-color: rgb(255, 0, 0);
    }

    .card.youngsters{

        border-top-color: rgb(24, 5, 59);
    }

    .card:hover {
        background-color: rgba(0, 123, 255, 0.384);
    }
    .info {
        padding: 1rem;
        text-align: center;
        font-size: 1.3rem;
    }
    .name {
        color: rgba(255, 255, 255, 0.445);

    }
    .birthday {
        font-weight: 300;
        font-size: 1rem;
    }

    .age {
        font-weight: 300;
        font-size: 1rem;
    }
    .year-title {
        color: #ffffffd3;
    }
    .footer-card {
        display: flex;
    }
    .btn {
        padding: .75rem 2rem;
        color: rgb(255, 255, 255);
        background-color: rgb(31, 31, 31);
        width: 50px;
        flex-grow: 1;
        text-align: center;
        transition: .5s;
        font-size: 1rem;
    }
    .btn.edit {
        background: rgb(0, 200, 255);
    }
    .btn.remove {
        background: rgba(255, 0, 0, 0.23);
    }
    .btn:hover {
        opacity: .3;
        cursor: pointer;;
    }
</style>
