<script lang="ts">
    import { movies, emptyMovie } from './../movie-list'
    import Modal from './../components/modal.svelte'
    import '../fonts.css';

    const date = new Date();
    const month = date.getMonth();
    let day = $state(date.getDate());
    let isOpen = $state(month !== 11);
    let movie = $derived(getCurrentMovie(day));
    let showModal = $state(month !== 11);
    if (month === 11) openDoor();

    function getCurrentMovie(day: number) {
        if (month !== 11) return emptyMovie;
        if (day < 1 || day > 30) return emptyMovie;
        return movies[day - 1] || emptyMovie;
    }

    function incrementDay() {
        if (day < 30) day++;
    }

    function decrementDay() {
        if (day > 1) day--;
    }

    function openDoor() {
        setTimeout(() => {
            isOpen = true;
        }, 6000);
    }
</script>

<header>
    <h1 class="title">🎄 Ortenisa's Navidario 🎄</h1>
</header>
<nav class="disappear">
    <button class="arrow-button" type="button" onclick={decrementDay} aria-label="arrow-button"><i  class="arrow left"></i></button>
    <button class="arrow-button" type="button" onclick={incrementDay} aria-label="arrow-button"><i class="arrow right"></i></button>
</nav>
<main>
    <div class="door {isOpen ? 'open' : 'closed'}">
        <div class="behind-door {isOpen ? '' : 'disappear'}">
            {#if month === 11}<h2>{movie.title}</h2>{/if}
            <p class="description">{movie.description}</p>
        </div>
        <img class="behind-door" src={movie.path} alt={movie.title} />
        <div class="day-number {isOpen ? 'disappear' : ''}">{day}</div>
    </div>
</main>
<audio autoplay loop>
    <source src="/christmas-spirit.mp3" type="audio/mp3" />
    Your browser does not support the audio element.
</audio>
{#if showModal}<Modal bind:showModal></Modal>{/if}


<style>
    :global(body) {
        color: white;
        padding: 0;
    }

    .title {
        font-family: "Christmas Comeback", sans-serif;
        font-size: 3rem;
    }

    header {
        text-align: center;
        padding-bottom: 2rem;
    }

    nav {
        display: flex;
        justify-content: flex-end;
        gap: 1rem;
        padding: 2rem;
    }

    .arrow-button {
        background-color: transparent;
        border: none;
        cursor: pointer;
    }

    main {
        display: flex;
        justify-content: center;
    }
    .door {
        position: relative;
        display: flex;
        justify-content: center;
        border: solid #5C4033 5px;
        justify-content: space-around;
        align-items: center;
        flex-direction: row-reverse;
        gap: 1rem;
        width: 50%;
        font-family: "Lato", sans-serif;
    }

    .open {
        background-color: transparent;
        border: none;
    }

    .closed {
        background: url('/wood-background.jpg') no-repeat 0 0 scroll;
        background-size: 100% 100%;
        border-radius: 5px;
    }

    .behind-door {
        z-index: -1;
    }

    .day-number {
        position: absolute;
        top: 50%;
        left: 50%;
        font-size: 5rem;
        transform: translate(-50%, -50%);
        font-family: 'Deer Snow', sans-serif;
        color: #c60f0f;
    }

    .disappear {
        display: none;
    }

    h2 {
        text-align: center;
    }

    .description {
        width: 300px;
        font-family: 'Lato Light', sans-serif;
        text-align: center;
    }

    img {
        max-width: 50%;
    }

    @media (max-width: 768px) {
        .title {
            font-size: 2rem;
        }

        .door {
            flex-direction: column;
            width: 100%;
        }

        img {
            max-width: 100%;
        }
    }

    .arrow {
        border: solid white;
        border-width: 0 3px 3px 0;
        display: inline-block;
        padding: 3px;
    }
    .right {
        transform: rotate(-45deg);
        -webkit-transform: rotate(-45deg);
    }
    .left {
        transform: rotate(135deg);
        -webkit-transform: rotate(135deg);
    }
</style>