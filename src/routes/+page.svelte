<script>
  // @ts-nocheck
  import ImageViewer from "../components/ImageViewer.svelte";
  import Banner from "../components/Banner.svelte";
  import "@shopify/polaris/build/esm/styles.css";
  import jsBeautify from "js-beautify";
  let value = "";
  let imageFuture = Promise.resolve(null);
  $: {
    imageFuture = calculateImage(value);
  }
  async function calculateImage(value) {
    try {
      let parser = new DOMParser();
      let parsed = parser.parseFromString(value, "text/html");
      let img = parsed.querySelector("img");
      if (!img) {
        return null;
      }
      let source = img?.src;
      let style = img?.getAttribute("style");
      let ratio =
        100 -
        Math.round(
          (await dataUrlToBytes(source)).length / (source.length / 100)
        );
      img.src = `{{ 'etbis.png' | file_img_url: 'master' }}`;
      img.loading = "lazy";
      let snippet = jsBeautify.html(parsed.body.innerHTML);
      return {
        source,
        snippet,
        ratio,
        style,
      };
    } catch (error) {
      throw error;
    }
  }

  async function dataUrlToBytes(dataUrl) {
    const res = await fetch(dataUrl);
    return new Uint8Array(await res.arrayBuffer());
  }
  function translate(text) {
    return text;
  }
</script>

<svelte:head>
  <title>{translate("Etbis Image Generator")}</title>
</svelte:head>

<div
  class="Polaris-AlphaStack Polaris-AlphaStack--fullWidth"
  style:--pc-stack-align="start"
  style:--pc-stack-gap-xs="var(--p-space-4)"
>
  <div class="Polaris-FormLayout">
    <div class="Polaris-FormLayout__Item">
      <div class="Polaris-Labelled__LabelWrapper">
        <div class="Polaris-Label">
          <label id="valueLabel" for="value" class="Polaris-Label__Text"
            >{translate("Etbis HTML Code")}</label
          >
        </div>
      </div>
      <div class="Polaris-Connected">
        <div class="Polaris-Connected__Item Polaris-Connected__Item--primary">
          <div
            class="Polaris-TextField Polaris-TextField--hasValue Polaris-TextField--multiline"
          >
            <textarea
              autocomplete="off"
              class="Polaris-TextField__Input"
              rows="6"
              aria-labelledby="valueLabel"
              aria-invalid="false"
              aria-multiline="true"
              bind:value
            />
            <div class="Polaris-TextField__Backdrop" />
          </div>
        </div>
      </div>
    </div>
    {#await imageFuture}
      <span>{translate("Loading")}</span>
    {:then image}
      {#if !image}
        <div class="Polaris-FormLayout__Item">
          <Banner />
        </div>
      {:else}
        <ImageViewer {image} />
      {/if}
    {:catch err}
      {err}
    {/await}
  </div>
</div>
