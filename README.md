# Displaying TIFFs with UTIF.js

This is a demo using [UTIF.js](https://github.com/photopea/UTIF.js) to decompress and display TIFF images in a browser. In this particular demo I'm using 300dpi B&W images with Group IV compression, which are the vast majority of TIFFs that I deal with in document imaging.

I am impressed with the size, speed, and reliability UTIF.js. It handles, proper specification compliant TIFFs fine. It also manages to deal with of the poorly formatted TIFFs I've come across, TIFFs that will not work with C and Java libraries that I've tried.

The TIFF specification can be [downloaded from Adobe](https://www.adobe.io/content/dam/udp/en/open/standards/tiff/TIFF6.pdf).

## A word about Canvas vs. Image

If your TIFFs can be displayed 1:1 in the browser, you can use a Canvas, or the `UTIF.replaceIMG()` method. However if your images must be scaled down, consider using an Image.

Browsers do not always handle Canvas and Image similarly. Canvas in Chrome, Firefox, and Edge looses definition when scaled down, vs. Image which does some smoothing. The comparisions below show screen captures from Chrome of a portion of a Group IV 300dpi Letter sized image when reduced to approximately one third its normal style. The left hand side shows the Canvas scaled; the right hand side shows the Image scaled.

![Alt "Detail Canvas vs. Image, sample 1"](https://github.com/johnthad/utif-demo/blob/master/compare/compare0.png 'Detail Canvas vs. Image, sample 1')

![Alt "Detail Canvas vs. Image, sample 2"](https://github.com/johnthad/utif-demo/blob/master/compare/compare1.png 'Detail Canvas vs. Image, sample 2')

Interestingly, Safari displays both Canvas and Image clearly, like the right hand side of the samples above. IE9 and IE11 looks like the left side regarless.

**NOTE:** In the file `UTIF-img.js` I have modified lines 1079-82 to use Image instead of Canvas in the `UTIF.replaceIMG()` method.

## Instructions

Clone or otherwise download this demo into a folder on your workstation or laptop.

Change directory to the folder and run `npm install`. If you are not using npm, you can download `UTIF.js` from [UTIF.js](https://github.com/photopea/UTIF.js), and alter the script paths accordingly.

I am able to open `index.html` from a `file://` URL using Firefox, but this causes CORS issues in some browsers. If `file://` works for you, fine. Otherwise, copy into your `~/Sites` or `~/public_html` directory, navigate to the location with your browser, and try out the samples.

## Update

Now using UTIF.js 3.1 via npm. Now with LZW support, and my canvas mods.

The file `utif-bundle.js` was created to bundle UTIF.js and Pako.js (for zlib). This was done on the command line from a UTIF.js repo using the command `browserify UTIF.js --s UTIF -o utif-bundle.js`. Note that it is _much larger_ than straigt UTIF.js: 282Kb vs 60Kb, so if you don't need `Inflate` and `Deflate`, stick with UTIF.js.
