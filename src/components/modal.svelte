<script lang="ts">
    import '../fonts.css';

    let { showModal = $bindable() }: { showModal: boolean } = $props() 

    let text1 = 'Hola Ortenisa! Soy tu navidario (calendario de Navidad).'
    let text2 = 'A partir del 1 de diciembre cada día te traeré una recomendación de película relacionada con la Navidad. Así no tienes que preocuparte por pasar horas de elegir una y ahorras tiempo valioso 😉. También espero que haya alguna película que no hayas visto y que pueda convertirse en una nueva favorita.';
    let text3 = 'Que empiece el viaje. Disfruta!'
    let dialog: HTMLDialogElement | undefined = $state();

    $effect(() => {
        if (showModal) {
            dialog?.showModal();
        } else {
            dialog?.close();
        }
    });
</script>

<dialog bind:this={dialog} onclose={() => {showModal = false;}} onclick={(e) => {if (e.target === dialog) showModal = false;}}>
    <div class="texts">
        <div class="text">{text1}</div>
        <div class="text">{text2}</div>
        <div class="text">{text3}</div>
    </div>
    <button onclick={() => {dialog?.close()}}>Entendido!</button>
</dialog>

<style>
    dialog {
        width: 70%;
        height: 400px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        font-family: 'Lato Light', sans-serif;
        color: white;
        border: none;
        text-align: center;
        background-image: url('/christmas-background.jpg');
        background-size: cover;
        background-repeat: no-repeat;
        overflow: hidden;
    }

    .text {
        padding-bottom: 1rem;
    }

    button {
        background-color: #7f0808;
        border: solid 3px white;
        border-radius: 3px;
        font-family: 'Lato', sans-serif;
        font-size: 1.2rem;
        color: white;
        padding: 1rem 2rem;
        cursor: pointer;
    }

    @media (max-width: 768px) {
        dialog {
            width: 100%;
        }
    }
</style>