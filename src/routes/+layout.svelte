<script>
  // @ts-nocheck
  function translate(text) {
    return text;
  }
</script>

<div class="Polaris-Page Polaris-Page--narrowWidth">
  <div
    class="Polaris-Box"
    style="--pc-box-padding-block-end-xs:var(--p-space-400);--pc-box-padding-block-end-md:var(--p-space-500);--pc-box-padding-block-start-xs:var(--p-space-400);--pc-box-padding-block-start-md:var(--p-space-500);--pc-box-padding-inline-start-xs:var(--p-space-400);--pc-box-padding-inline-start-sm:var(--p-space-0);--pc-box-padding-inline-end-xs:var(--p-space-400);--pc-box-padding-inline-end-sm:var(--p-space-0);position:relative"
  >
    <div
      class="Polaris-Page-Header Polaris-Page-Header--isSingleRow Polaris-Page-Header--hasNavigation Polaris-Page-Header--mediumTitle"
    >
      <div class="Polaris-Page-Header__Row">
        <div class="Polaris-Page-Header__TitleWrapper">
          <h1 class="Polaris-Header-Title">
            {translate("Etbis Image Generator")}
          </h1>
        </div>
      </div>
    </div>
    <div class="Polaris-Page--divider" />
    <slot />
  </div>
</div>
