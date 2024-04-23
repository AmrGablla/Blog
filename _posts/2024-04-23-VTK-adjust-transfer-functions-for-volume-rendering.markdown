---
layout: post
title:  "VTK adjust transfer functions for volume rendering"
date:   2024-04-23 14:30:55 +0200 
---
# VTK adjust transfer functions for volume rendering


In the context of utilizing the Cornerstone library for rendering medical images in 3D volume or leveraging the VTK library directly, one inevitably encounters the challenge of implementing the widely-used WW/WL tool. This tool enables radiologists to adjust the volume to focus within a specific window.

Render volume in VTK have many properties and manipulating this properties change the rendered volume in the way that give the user the control that need.


this properties contains:

- color transfer function
- scalar opacity
- gradient opacity
- interpolation
- shade
- ambient
- diffuse
- specular
- specular power

All this properties effect in the rendering but i'll focus with color transfer, scalar opacity and gradient opacity that what we need for this adjust of the volume.

## Color transfer function and scalar opacity 
Color transfer function maps scalar values (typically representing tissue density or some other physical property) to colors for visualization purposes.
And scalar opacity control the opacity of this scalar values.

Example of that this values:
-3024 0 0 0 
-16.4458 0.729412 0.254902 0.301961
641.385 0.905882 0.815686 0.552941 
3071 1 1 1

this four sRGB points control the color from voxels values -3024 to -16.4458 to be colored with 0 0 0 (black color)

and it is scalar opacity values:
-3024 0 
-16.4458 0 
641.385 0.715686 
3071 0.705882

and will be hidden cause the opacity is 0 totally hidden.

So you can the values represent a function for range of points and set it is color and opacity.

In cornerstone that can be done with applyPreset function:

``` js
const preset = {
	name: 'CT-Bone',
	gradientOpacity: '4 0 1 255 1',
	specularPower: '10',
	scalarOpacity: '8 -3024 0 -16.4458 0 641.385 0.715686 3071 0.705882',
	specular: '0.2',
	shade: '1',
	ambient: '0.1',
	colorTransfer:
	'16 -3024 0 0 0 -16.4458 0.729412 0.254902 0.301961 641.385 0.905882 0.815686 0.552941 3071 1 1 1',
	diffuse: '0.9',
	interpolation: '1',
}

utilities.applyPreset(  
    volumeActor.actor,  
    preset 
);
```

And in VTK you can did it like this:

``` js
import vtkColorTransferFunction from '@kitware/vtk.js/Rendering/Core/ColorTransferFunction';

// Create a color transfer function
const colorTransferFunction = vtkColorTransferFunction.newInstance();
colorTransferFunction.addRGBPoint(-3024, 0.0, 0.0, 0.0); colorTransferFunction.addRGBPoint(-16.4458, 0.729412, 0.254902, 0.301961); colorTransferFunction.addRGBPoint(641.385, 0.905882, 0.815686, 0.552941); colorTransferFunction.addRGBPoint(3071, 1.0, 1.0, 1.0);

// Apply the color transfer function to the volume property
const volumeProperty = vtk.VolumeProperty.newInstance();
volumeProperty.setRGBTransferFunction(0, colorTransferFunction);

```


This preset value show the 