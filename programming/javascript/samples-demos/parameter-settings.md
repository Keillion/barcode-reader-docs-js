---
layout: default-layout
title: Dynamsoft Barcode Reader for JavaScript - Parameter Settings Samples
description: Dynamsoft Barcode Reader SDK for JavaScript - Parameter Settings
keywords: javascript, js, barcode, vanilla, parameter
noTitleIndex: true
breadcrumbText: Parameter Settings
---

# JavaScript Parameter Settings Samples

Dynamsoft Barcode Reader JavaScript SDK (hereafter called "the library") is based on Dynamsoft's algorithm in ROI (region of interest) locating and decoding. The algorithm is very flexible and has many configurable parameters. In this article, we'll take a look at how the library makes use of these parameters.

## Specify the Barcode Types and Number of Barcodes Per Image

In most cases, an application only needs to process one or several predetermined types of Barcodes. Also, the algorithm is more efficient when it knows how many barcodes are expected on an image. The following code shows how to read 2 QR codes on an image.

```javascript
let settings = await scanner.getRuntimeSettings();
settings.barcodeFormatIds = Dynamsoft.DBR.EnumBarcodeFormat.BF_QR_CODE;
settings.expectedBarcodesCount = 2;
await scanner.updateRuntimeSettings(settings);
```

The following official sample showcases the same features.

* <a target = "_blank" href="https://dynamsoft.github.io/barcode-reader-javascript-samples/3.settings/1.barcodeFormats-expectedBarcodes.html">Specify Barcode Types and Count - Demo</a>
* <a target = "_blank" href="https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/master/3.settings/1.barcodeFormats-expectedBarcodes.html">Specify Barcode Types and Count - Source Code</a>

## Set Localization and Binarization Modes

Localization and binarization are two essential steps in the barcode reading process. 

* Localization Modes

Localization modes specify how the algorithm scan the image in order to find a barcode. At present, 7 modes are available: "Connected Blocks", "Statistics", "Lines", "Scan Directly", "Statistics Marks", "Statistics Postal Code" and "Center". More information can be found [here](https://www.dynamsoft.com/barcode-reader/parameters/reference/localization-modes.html?ver=latest). A barcode reading session will exhaust all set modes until the intended number of barcodes are found. In other words, the more modes you set, the harder the algorithm tries to find barcodes. The following code shows how to set multiple modes.

```javascript
let settings = await scanner.getRuntimeSettings();
settings.localizationModes = [2, 16, 4, 8, 32, 64, 0, 0];
await scanner.updateRuntimeSettings(settings);
```

Note that each mode is represented by a number.

Read more on [How to use different localization modes](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/how-to-set-localization-modes.html).

* Binarization Modes

Binarization modes specify how the algorithm binarizes a colored or gray image. Right now, there are only two modes available: "Local Block" and "Threshold". More information can be found [here](https://www.dynamsoft.com/barcode-reader/parameters/reference/binarization-modes.html?ver=latest).

For each mode, there are a few arguments to fine-tune it for best performance. Read more on [How to configure the binarization parameters](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/how-to-set-binarization-modes.html?ver=latest).

The following official sample demonstrates how to set Localization and Binarization modes.

* <a target = "_blank" href="https://dynamsoft.github.io/barcode-reader-javascript-samples/3.settings/2.localizationModes-binarizationModes.html">Localization and Binarization - Demo</a>
* <a target = "_blank" href="https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/master/3.settings/2.localizationModes-binarizationModes.html">Localization and Binarization - Source Code</a>

## Set Deblur Modes and Scale-up Modes

* Deblur Modes

The barcode reader often needs to handle blurry images, setting the deblur modes will help the algorithm better process them. In the library, there are 7 available modes: "Direct Binarization", "Threshold_Binarization", "Gray_Equalization", "Smoothing", "Morphing", "Deep_Analysis" and "Sharpening". More information can be found [here](https://www.dynamsoft.com/barcode-reader/parameters/reference/deblur-modes.html?ver=latest). A barcode reading session will exhaust all set modes until the intended number of barcodes are found. In other words, the more modes you set, the harder the algorithm tries to find barcodes. The following code shows how to set multiple deblur modes.

```javascript
let settings = await scanner.getRuntimeSettings();
settings.deblurModes = [1, 2, 4, 8, 0, 0, 0, 0, 0, 0];
await scanner.updateRuntimeSettings(settings);
```

* Scale-up Modes

In many cases, the barcodes appear very small on the image and makes it difficult to read. The scale-up modes can be used to enlarge such barcodes before reading them. In the library, there are 2 available modes: "Linear_Interpolation" and "Nearest_Neighbour_Interpolation". More information can be found [here](https://www.dynamsoft.com/barcode-reader/parameters/reference/scale-up-modes.html?ver=latest).

For each mode, there are a few arguments to fine-tune it for best performance. Read more on [How to read barcodes with small module sizes](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/how-to-set-scaleup-modes.html?ver=latest).

The following official sample demonstrates how to set Deblur modes and Scale-up modes.

* <a target = "_blank" href="https://dynamsoft.github.io/barcode-reader-javascript-samples/3.settings/3.blurred-small-barcodes.html">Deblur Modes and Scale-Up Modes - Demo</a>
* <a target = "_blank" href="https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/master/3.settings/2.localizationModes-binarizationModes.html">Deblur Modes and Scale-Up Modes - Source Code</a>

## Deformation-Resisting Modes and Barcode-Complement Modes

* Deformation-Resisting Modes

As the name suggests, deformation-resisting modes deal with deformed barcocdes. Read more on [How to deal with deformed barcodes](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/resist-deformation.html?ver=latest).

For now, there is only one available mode: "General".

The following code enables deformation resisting.

```javascript
let settings = await scanner.getRuntimeSettings();
settings.furtherModes.deformationResistingModes = [2, 0, 0, 0, 0, 0, 0, 0];
await scanner.updateRuntimeSettings(settings);
```

* Barcode-Complement Modes

QR codes and Data Matrix codes can be read even if they are incomplete due to reasons like misprinting. Read more on [How to decode incomplete barcodes](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/how-to-set-barcode-complememt-modes.html?ver=latest).

The parameter for this case is called [ `BarcodeComplementMode` ](https://www.dynamsoft.com/barcode-reader/parameters/reference/barcode-complement-modes.html?ver=latest) which has only one available mode at present: "General". 

The following code enables incomplete barcode reading.

```javascript
let settings = await scanner.getRuntimeSettings();
settings.furtherModes.deformationResistingModes = [2, 0, 0, 0, 0, 0, 0, 0];
await scanner.updateRuntimeSettings(settings);
```

The following official sample showcases deformation resisting and barcode complementing.

* <a target = "_blank" href="https://dynamsoft.github.io/barcode-reader-javascript-samples/3.settings/4.deformed-incomplete-barcodes.html">Deformation-Resisting Modes and Barcode-Complement Modes - Demo</a>
* <a target = "_blank" href="https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/master/3.settings/4.deformed-incomplete-barcodes.html">Deformation-Resisting Modes and Barcode-Complement Modes - Source Code</a>

## Define or Detect the Region of Interest

When reading barcodes from a video input, the barcode normally takes up only a small portion of the video frame. If the barcode always appear around the same spot, we can set a limited region around it as the ROI (Region of Interest) to speed up the barcode reading process. With the library, there are two ways to do this.

* Manually define the ROI

If the ROI is predetermined in the use case, we can manually set the limit. For example, the following only reads 25% of the central area.

```javascript
let settings = await scanner.getRuntimeSettings();
settings.region.regionMeasuredByPercentage = 1;
settings.region.regionLeft = 25;
settings.region.regionTop = 25;
settings.region.regionRight = 75;
settings.region.regionBottom = 75;
await scanner.updateRuntimeSettings(settings);
```

* Automatically detect the ROI

To let the algorithm detect the ROI automatically, we can set the parameter [ `RegionPredetectionModes` ](https://www.dynamsoft.com/barcode-reader/parameters/reference/region-predetection-modes.html?ver=latest) which has four available modes: "General", "General_RGB_Contrast", "General_Gray_Contrast" and "General_HSV_Contrast". 

For each mode, there are a few arguments to fine-tune it for best performance. Read more on [How To Use Region Predetection](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/how-to-use-region-predetection.html?ver=latest).

The following official sample showcases both ways to specify ROI.

* <a target = "_blank" href="https://dynamsoft.github.io/barcode-reader-javascript-samples/3.settings/5.regionOfInterest-regionPredetection.html">Define or Detect the Region of Interest - Demo</a>
* <a target = "_blank" href="https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/master/3.settings/5.regionOfInterest-regionPredetection.html">Define or Detect the Region of Interest - Source Code</a>
