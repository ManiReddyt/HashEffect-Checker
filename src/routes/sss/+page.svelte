<script>
  import { sssShares, sssVerify } from "../../api";
  import { onMount } from "svelte";

/**
   * @type {any}
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
    

    <table class="flex justify-center mt-5">
      <tbody class="border bg-slate-100 px-2">
        <tr class="space-x-2">
          <td class="w-[1/2] text-center pr-4 ">K</td>
          <td class="w-1/2 text-left pl-4">{data.k}</td>
        </tr>
        <tr class="">
          <td class="w-[1/2] text-center pr-4">N</td>
          <td class="w-1/2 text-left pl-4">{data.n}</td>
        </tr>
        {#each data.shares as share, index}
          <tr>
            <td class="w-[1/2] text-right pr-4">Share {index}</td>
            <td class="w-1/2 text-left pl-4">{Number("0x" + share.value.value)}</td>
          </tr>
        {/each}
      </tbody>
    </table>
	<div class="flex justify-center mt-5">
		<input
		  bind:value={secret}
		  placeholder="Enter your secret"
		  class="border bg-gray-100"
		/>
	</div>
	<div class="flex justify-center mt-5">

		<button class="bg-blue-500 px-1" on:click={submitSecret}>{status}</button>
	</div>
  {:else}
    <div>Loading...</div>
  {/if}
</div>
