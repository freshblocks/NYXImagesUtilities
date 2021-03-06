# NYXImagesUtilities #

This is a project for iOS which regroups a collection of useful UIImage categories to handle operations such as filtering, blurring, masking, reflecting, resizing, rotating, saving.
***NYXImagesUtilities*** requires at least iOS 4.0, I don't intend to support older versions.


## Installation ##

- Link with **QuartzCore** framework then **#import &lt;QuartzCore/QuartzCore.h&gt;** in your *Prefix.pch* file.
- Add the *Categories* and *Helper* directories to your project, and you are good to go !

If you want to use the saving category you must also link with :

- **ImageIO.framework**
- **MobileCoreServices.framework**

By default the methods return auto-released objects, if you want them to return retained objects in order to manage memory yourself, just uncomment the <code>kNYXReturnRetainedObjects</code> constant in **NYXImagesHelper.h**.


## UIImage+Filtering ##

This category allows you to apply filters on a UIImage object, currently there are 3 filters : Sepia, Grayscale and changing opacity.

<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_original.png" alt="Sepia image" width="210" height="158" style="margin-left:auto;margin-right:auto;display:block;" />

Using these filters is very easy :

	UIImage* sepia = [myImage sepia];
	UIImage* gray = [myImage grayscale];
	UIImage* transparent = [myImage opacity:0.5f];

<div style="margin-left:auto;margin-right:auto;display:block;">
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_sepia.jpg" width="210" height="158" />
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_grayscale.jpg" width="210" height="158" />
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_opacity.jpg" width="210" height="158" />
</div>


## UIImage+Blurring ##

This category is composed of a single method which was originally written by Jeff Lamarche (@jeff_lamarche), you can read about it <a href="http://iphonedevelopment.blogspot.com/2010/08/uiimage-blur.html">here</a>.

It allows to blur an image by a given factor.

	UIImage* blur = [myImage blurredCopyUsingGuassFactor:5 andPixelRadius:5];

<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_blur.jpg" width="210" height="158" style="margin-left:auto;margin-right:auto;display:block;" />


## UIImage+Masking ##

This category is composed of a single method which allow to mask an image, you just have to create the mask you desire.

	UIImage* masked = [myImage maskWithImage:[UIImage imageNamed:@"mask.png"]];
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_mask.png" width="210" height="158" style="margin-left:auto;margin-right:auto;display:block;" />


## UIImage+Reflection ##

This category was written by Matthias Tretter (@myell0w) and is composed of a single method to create a reflected image.

	UIImage* reflected = [myImage reflectedImageWithHeight:myImage.size.height fromAlpha:0.0f toAlpha:0.5f];
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_refl.jpg" width="210" height="315" style="margin-left:auto;margin-right:auto;display:block;" />


## UIImage+Resizing ##

This category can be used to crop or to scale images.


### Cropping ###

You can crop your image by 9 different ways :

1. Top left
2. Top center
3. Top right
4. Bottom left
5. Bottom center
6. Bottom right
7. Left center
8. Right center
9. Center

To crop an image object just call <code>-(UIImage*)cropToSize:(CGSize)newSize usingMode:(NYXCropMode)cropMode;</code> like this :

	UIImage* cropped = [myImage cropToSize:(CGSize){width, height} usingMode:NYXCropModeCenter];
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_cropcenter.jpg" width="210" height="158" style="margin-left:auto;margin-right:auto;display:block;" />

<code>NYXCropMode</code> is an enum type which can be found in the header file, it is used to represent the 9 modes above.

There is also a convenience method which crop from the top left corner by default : <code>-(UIImage*)cropToSize:(CGSize)newSize;</code>


### Scaling ###

You have the choice between two methods to scale images, the two methods will keep the aspect ratio of the original image.

	UIImage* scaled1 = [myImage scaleByFactor:0.5f];
	UIImage* scaled2 = [myImage scaleToFitSize:(CGSize){width, height}];
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_scale.jpg" width="200" height="150" style="margin-left:auto;margin-right:auto;display:block;" />


## UIImage+Rotating ##

With this category you can rotate or flip an UIImage object, flipping is useful if you want to create a reflect effect.

	UIImage* rotated1 = [myImage rotateInDegrees:217.0f];
	UIImage* rotated2 = [myImage rotateInRadians:M_PI_2];
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_rotate.png" width="210" height="202" style="margin-left:auto;margin-right:auto;display:block;" />

	UIImage* flipped1 = [myImage verticalFlip];
	UIImage* flipped2 = [myImage forizontalFlip];
<img src="http://www.cocoabyss.com/wp-content/uploads/2011/05/niu_flip.jpg" width="210" height="158" style="margin-left:auto;margin-right:auto;display:block;" />


## UIImage+Saving ##

This category allows you to save an UIImage object at a specified path or file URL, there are five types supported : BMP, GIF, JPG, PNG, TIFF.

To use it, you must link with **ImageIO.framework** and **MobileCoreServices.framework**.

	[myImage saveToURL:url type:NYXImageTypeJPEG backgroundFillColor:nil];
	[myImage saveToPath:path type:NYXImageTypeTIFF backgroundFillColor:[UIColor yellowColor]];

There is also two other methods which take only the path or URL as parameter and save the image in PNG, because it's the preferred format for iOS.

If your image contains transparent zone and you save it in a format that doesn't support alpha, a fill color will be used, if you don't specify one, the default color will be white.


## License ##

***NYXImageUtilities*** is released under the Simplified BSD license, see LICENSE.txt.

I hope you will find this useful, if you would like to see more features you can send me an email.

Benjamin Godard.

Blog : <http://www.cocoabyss.com/>

Twitter : @Nyx0uf
