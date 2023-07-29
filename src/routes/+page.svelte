<script>
  import {page} from '$app/stores';
</script>

<section class="">
  <div class="w-fit mx-auto">
    <h1 class="mx-auto text-4xl font-bold ">
      Welcome to <span class="text-blue-500">HashEffect Test Tool</span> 
    </h1>
  </div>
    <nav class="w-fit mx-auto mt-5">
      <ul class="flex text-center space-x-5 mt-2 font-medium">
        <li aria-current={$page.url.pathname === '/sss' ? 'page' : undefined}>
          <a href="/sss">SSS</a>
        </li>
        <li aria-current={$page.url.pathname === '/vss' ? 'page' : undefined}>
          <a href="/vss">VSS</a>
        </li>
        <li aria-current={$page.url.pathname === '/schnor' ? 'page' : undefined}>
          <a href="/schnor">SCHNOR</a>
        </li>
      </ul>
    </nav>
</section>

<style lang="postcss">
  /* :global(html) {
    background-color: theme(colors.gray.100);
  } */
  section {
    /* display: flex; */
    /* align-items: center; */
    /* flex-direction: column; */
    /* margin-top: 30px; */
  }
</style>
