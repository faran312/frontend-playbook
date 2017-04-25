# Best practices when dealing with images for the Web

In a front-end workflow we typically deal with two kinds of images:

* **Icons, logos, buttons and other graphical elements** that are part of the User Interface of the page. These are usually managed by the frontend, and so they are stored with the rest of resources (templates, CSS, JS). Like those resources, they may be shared between many different pages.

* **Content images**. These are unique to a page (or a handful of pages). They will be usually provided from a database or a content management system.

Most best practices are common to both categories.

## Formats

### What format to use

* Use SVGs whenever you want to display a vector image.
* Use JPEGs for photo images, or images with many little details.
* Use PNGs for graphs and other images with large areas of the same colour. Also for images that require transparency.

### JPEG images

When encoding JPEG images:

* Use progressive encoding. Progressive JPEGs provide a better user experience and, most of the time, are smaller than baseline. See this [yeoman issue](https://github.com/yeoman/yeoman/issues/810) for further details.
* Use [4:2:0](https://en.wikipedia.org/wiki/Chroma_subsampling#4:2:0) [chroma subsampling](https://en.wikipedia.org/wiki/Chroma_subsampling) whenever possible. This encodes the colour information at half the resolution of the luma, which may result in a perceptible loss of colour accuracy. This will usually generate much smaller images, so we suggest to create both of them and compare them visually for any loss of quality.

### PNG images

Always use the maximum compression level (9).

## Optimisation

* Make sure that you save images using an [sRGB](https://en.wikipedia.org/wiki/SRGB) ICC profile. Although modern browsers support images with ICCv2 profiles like [Adobe RGB](https://en.wikipedia.org/wiki/Adobe_RGB_color_space) and even [ProPhoto RGB](https://en.wikipedia.org/wiki/ProPhoto_RGB_color_space), colour space issues are extremely difficult to debug. Saving the images as sRGB and removing the colour profile is encouraged.
* Strip the metadata from the image. This includes:
    * EXIF data
    * Copyright information (unless required)
    * GPS data
    * Colour profiles
    * Thumbnails in JPEGs
    * Comments
    * Etc.
* Set appropriate cache headers for the images.