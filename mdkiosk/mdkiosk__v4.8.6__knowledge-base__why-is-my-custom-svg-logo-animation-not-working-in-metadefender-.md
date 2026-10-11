<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-is-my-custom-svg-logo-animation-not-working-in-metadefender- -->

# Why is my custom SVG logo animation not working in MetaDefender Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to **MetaDefender Kiosk** releases on Windows and Linux

## [**Issue:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-is-my-custom-svg-logo-animation-not-working-in-metadefender-#issue)

Custom SVG logo with rotation animation implemented using JavaScript is not working in MetaDefender Kiosk. The logo **appears static in the preview** and on the Kiosk console.

## [**Resolution:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-is-my-custom-svg-logo-animation-not-working-in-metadefender-#resolution)

Use **SMIL** (Synchronized Multimedia Integration Language) or **CSS** to construct the animation within the SVG file. MetaDefender Kiosk supports the `<animateTransform>` tag embedded directly within the image for animations. Avoid using JavaScript within a `<script>` block, as it is not supported due to security concerns.

## [**References:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-is-my-custom-svg-logo-animation-not-working-in-metadefender-#references)

You can refer to the example repository: [n3r4zzurr0/svg-spinners: A collection of 24 x 24 dp SVG spinners! (CSS & SMIL)](https://github.com/n3r4zzurr0/svg-spinners).

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
