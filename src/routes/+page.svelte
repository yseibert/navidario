<script lang="ts">
    import { movies } from './../movie-list'

    const date = new Date();
    const month = date.getMonth();
    const day = date.getDate();
    const movie = getCurrentMovie();

    function getCurrentMovie() {
        return movies.find(movie => movie.id === day) || { id: 0, title: 'None', path: '', description: ''};
    }
</script>

<header>
    {#if month === 11}
        <p class="title">Para el día {day} de diciembre tu película será...</p>
        <img src={movie.path} alt={movie.title} />
    {:else}
        <p class="title">Tienes que tener un poco más de paciencia</p>
    {/if}
</header>

<style>
    header {
        text-align: center;
    }

    .title {
        color: white
    }
</style>