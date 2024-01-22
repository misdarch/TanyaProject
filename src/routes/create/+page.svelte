<!-- /create -->
<script>
    let cardListCount = 0
    let cardList = [
        {
            index: 0,
            isExpand: false,
            askText : "",
            ansType : "radio",
            ansList: [{
                id: 0,
                value: ""
            }],
            ansListCount: 0,
            essai: ""
        }
    ]
</script>

{JSON.stringify(cardList)}
<div class="scrollable">
    {#each cardList as card}
    <div class={`card pure-form`}>
        <div class="card-content" on:click={() => {
            card.isExpand = true
        }} on:mouseleave={() => {
            setTimeout(() => {card.isExpand = false}, 200)
        }} on:focus={() => {}} >
            
            <textarea class="askText" placeholder="Masukkan pertanyaan..." on:change={e => {card.askText = e.target.value}} />
            <label for="ansType">Tipe pertanyaan:</label>
            <select name="ansType" id="type" bind:value={card.ansType}>
                <option value="radio">Pilihan Ganda</option>
                <option value="list">Multi Pilihan</option>
                <option value="text">Essai</option>
            </select>
            
            <!-- Temporal Visible Area -->
            <div class="extendDisplay" style={card.isExpand ? "display: block" : ""}>
                {#if card.ansType === "radio"}
                    <div class="typeGroup">
                      <!--  {JSON.stringify(card)} -->
                        {#each card.ansList as list}
                        <div>
                        <input type="radio" name={`${card.index}rad`} id={list.id} />
                        <label for={list.id}>
                            <input type="text" on:change={e => {
                                list.value = e.target.value
                            }} />
                        </label>
                        </div>
                        {/each}
                    </div>
                {/if}
                
                {#if card.ansType === "list"}
                    <div class="typeGroup">
                      <!--  {JSON.stringify(card)} -->
                        {#each card.ansList as list}
                        <div>
                        <input type="checkbox" name={`${card.index}rad`} id={list.id} />
                        <label for={list.id}>
                            <input type="text" on:change={e => {
                                list.value = e.target.value
                            }} />
                        </label>
                        </div>
                        {/each}
                    </div>
                {/if}
                
                {#if card.ansType === "text"}
                    <div class="typeGroup">
                        <textarea rows="8" bind:value={card.essai} placeholder="Jawabanmu disini..."/>
                    </div>
                {/if}
                {#if card.ansType !== "text"}
                <button class="pure-button pure-button-primary" on:click={() => {
                    card.ansListCount++
                    card.ansList.push({ id: card.ansListCount })
                    cardList = cardList
                }}>
                    Tambah
                </button>
                {/if}
            </div>
            <!-- Temporal Visible Area -->
        </div>
    </div>
    {/each}
    
    <button class="pure-button-primary pure-button" on:click={() => {
        cardListCount++
        cardList.push({
            index: cardListCount,
            isExpand: false,
            askText : "",
            ansType : "radio",
            ansList: [{
                id: 0,
                value: ""
            }],
            ansListCount: 0
        })
        cardList = cardList
    }}>
        Tambah Kartu
    </button>
</div>

<style>
    .scrollable {
        position: relative;
        top: 0;left: 0;
        height: 100lvh;
        overflow: scroll;
    }
    
    .askText {
        margin-bottom: 10px;
    }
    
    .card {
      width: 90%;
      border: 1px solid #ccc;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      margin: 2rem 0;
    }
    
    .card-content {
      padding: 15px;
    }
    
    .askText {
        width: 100%;
    }
    
    .extendDisplay {
        margin-top: 1.5rem;
        display: none;
    }
    
    .typeGroup {
        display: flex;
        flex-direction: column;
        gap: 5px;
    }
    
    .typeGroup div {
        display: flex;
        gap: 5px;
    }
    
    .typeGroup textarea {
        margin-bottom: 10px;
    }
</style>