<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/deep-cdr/image-limit-configurations -->

# Image limit configurations

Processing image is an expensive task, it can be utilized to DDoS the system, making the system be overloaded. Having proper image limit configurations helps to protect in this case.

**Image Size Limit (MB):** A JPG/PNG file with a few byte in file size can be decompressed to become a few to a hundred MB. Therefore, this configuration is applied for the **decompressed raw data size**.

**TIFF Size Limit (MB):** why do we separate PNG/JPG size limit from the TIFF size limit? The TIFF file processing is expensive when it uses Group 4 compression but not in the other format. Also, the TIFF raw data size is calculated in a different way from PNG/JPG. Therefore, using the same values with JPG/PNG configuration doesn't work well. This configuration is applied for the **decompressed raw data size**.

**GIF Layer Count Limit:** GIF processing performance depends on not only the number of layers but also the image dimension. For example, a GIF with 40000 layers with 1x1 (Width x Height) pixels is taking more time to process than a GIF with 400 layers with 100x100 pixels. In this case, we use a “**normalized**” version that combines the number of layers and image dimension, it is not the same as the original GIF layer count.

If the values in the files are over the limitation, the sanitization result will be **Sanitization Failed**
