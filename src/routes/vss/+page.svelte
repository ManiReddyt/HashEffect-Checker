<script>
  import { sssShares, sssVerify } from "../../api";
  import { onMount } from "svelte";

  /**
   * @type any
   */
  let data = null;
  let secret = "";
  let status = "Submit";
  onMount(async function () {
    try {
      const response = await fetch(sssShares);
      data = await response.json();
      console.log("data : ", data);
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  });

  async function submitSecret() {
    try {
      console.log("Object: ", { shares: data.shares, secret: secret });
      const response = await fetch(sssVerify, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ shares: data.shares, secret: secret }),
      });
      const res = await response.json();
      status = res.status;
      console.log("res : ", res);
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  }
</script>

<div>
  <div class="text-center text-3xl font-bold">SSS VERIFICATION</div>
  {#if data}
    <div>K={data.k}</div>
    <div>N={data.n}</div>
    <div>Prime={data.shares[0].value.prime}</div>
    {#each data.shares as share, index}
      <div>Share {index} : {Number("0x" + share.value.value)}</div>{/each}
    <input
      bind:value={secret}
      placeholder="enter your secret"
      class="bg-gray-100"
    />
    <button on:click={submitSecret}>{status}</button>
  {:else}
    <div>Loading...</div>
  {/if}
</div>
