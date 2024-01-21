<script>
    import "purecss"
    import Icon from "$lib/assets/favicon.png"
    let OpenMenu = false
    let ChangeMenu = () => OpenMenu = !OpenMenu
</script>

<nav>
    <button class={`burger ${OpenMenu ? "active" : ""}`} on:click={ChangeMenu}>
        <span></span>
        <span></span>
        <span></span>
    </button>
    <img alt="Logo Tanya" src={Icon} />
</nav>

<style>
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-sizing: border-box;
        margin: .5rem;
    }
    
    .burger {
      display: flex;
      flex-direction: column;
      cursor: pointer;
      background-color: transparent;
      border: none;
    }
    
    .burger span {
      display: block;
      width: 1.8rem;
      height: .2rem;
      background-color: #333;
      margin: .2rem 0;
      transition: 0.4s;
    }
    
    .burger.active span:nth-child(1) {
      transform: rotate(-45deg) translate(-.4rem, .45rem);
    }

    .burger.active span:nth-child(2) {
      opacity: 0;
    }

    .burger.active span:nth-child(3) {
      transform: rotate(45deg) translate(-.4rem, -.45rem);
    }
    
    img {
        position: relative;
        width: 2.5rem;height: 2.5rem;
    }
</style>

<slot />