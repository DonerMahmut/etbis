<script>
  //@ts-nocheck
  export let image;
  const copyContent = async () => {
    try {
      await navigator.clipboard.writeText(image.snippet);
    } catch (err) {
      alert(translate("Failed copy.."));
    }
  };

  async function saveImage() {
    const etbisImage = new Image();
    etbisImage.onload = () => {
      const canvas = document.createElement("canvas");
      canvas.width = etbisImage.naturalWidth;
      canvas.height = etbisImage.naturalHeight;
      canvas.getContext("2d").drawImage(etbisImage, 0, 0);
      ["webp", "png"].forEach((ext) => {
        canvas.toBlob(
          (blob) => {
            let filename = `etbis.${ext}`;
            const formatImage = new File([blob], filename, {
              type: blob.type,
            });
            let anchor = document.createElement("a");
            anchor.href = URL.createObjectURL(formatImage);
            anchor.download = filename;
            anchor.click();
          },
          `image/${ext}`,
          0.7
        );
      });
    };
    etbisImage.src = image.source;
    let anchor = document.createElement("a");
    anchor.href = image.source;
    anchor.download = "etbis.jpg";
    anchor.click();
  }

  function translate(text) {
    return text;
  }
</script>

<div class="Polaris-FormLayout__Item">
  <div class="Polaris-LegacyCard">
    <div class="Polaris-MediaCard">
      <div class="Polaris-MediaCard__MediaContainer">
        <img
          src={image.source}
          alt="Etbis"
          width="100%"
          height="100%"
          style:object-fit="cover"
          style:object-position="center"
        />
      </div>
      <div class="Polaris-MediaCard__InfoContainer">
        <div class="Polaris-LegacyCard__Section">
          <div
            class="Polaris-LegacyStack Polaris-LegacyStack--vertical Polaris-LegacyStack--spacingTight"
          >
            <div class="Polaris-LegacyStack__Item">
              <div class="Polaris-Labelled__LabelWrapper">
                <div class="Polaris-Label">
                  <label id="valueLabel" for="value" class="Polaris-Label__Text"
                    >{translate("Etbis Shopify Code")}</label
                  >
                </div>
              </div>
              <div class="Polaris-Connected">
                <div
                  class="Polaris-Connected__Item Polaris-Connected__Item--primary"
                >
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
                      value={image.snippet}
                    />
                    <div class="Polaris-TextField__Backdrop" />
                  </div>
                </div>
              </div>
            </div>
            <div class="Polaris-LegacyStack__Item">
              <div class="Polaris-MediaCard__ActionContainer">
                <div class="Polaris-ButtonGroup">
                  <div class="Polaris-ButtonGroup__Item">
                    <div class="Polaris-MediaCard__PrimaryAction">
                      <button on:click={saveImage} class="Polaris-Button">
                        <span class="Polaris-Button__Content">
                          <span class="Polaris-Button__Text"
                            >{translate("Download")}</span
                          >
                        </span>
                      </button>
                    </div>
                  </div>
                  <div class="Polaris-ButtonGroup__Item">
                    <div class="Polaris-MediaCard__PrimaryAction">
                      <button class="Polaris-Button" on:click={copyContent}>
                        <span class="Polaris-Button__Content">
                          <span class="Polaris-Button__Text"
                            >{translate("Copy code")}</span
                          >
                        </span>
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
