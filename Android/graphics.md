# [Graphics For Android Developers](https://youtu.be/xmFrEYbxoXg?si=J5rCWvAvCXluvIta)

Fringing in anti-aliasing is an unwanted colored outline or halo around smoothed edges, caused when semi-transparent transition pixels retain traces of an original background color.

Phones uses additive mixing and a combination of distance(distance is crucial so our eye can perceive the wanted color as if we zoom in too much we could even see those red, green blue 
dots on each pixel, so colors + distances = mixed colors) to paint colors, for example white is accomplished by very small pixels that have its RGB values set to max, each pixel has a little red green and blue light

RGB are the primary colors in digital screens, in art it is red yellow and blue. It exists additive and subtractive colors, digital screen uses additive, subtractive color exist in the 
physical world, light gets reflected over a paint depending on the nature of the paint, some paints are glossy, some are matte. The light that doesn’t get reflected, penetrates the paint 
and gets scattered, some of the light will get absorbed by the paints itself and some other will come out, for example in a red paint the light that comes out is the result of subtracting 
everything that is not red, so it does subtracting mixing, and then it gets back to additive mixing mode because light is coming out and our eyes mix those together in and additive way, 
but that is real world physical painting, but digital screens work differently. 

Our eyes are poorly on blue light, and they are most sensitive to green light. Colors/lights are part of the radio spectrum and our eyes are like radio receptors, they perceive radio waves, 
but only some waves. Eyes have something called cones which are cells sensitive to some specific type of light there is three types of cones, short, medium and long, each cone can perceive 
a part of the radio spectrum. 

But how could we define a color, like red for example, is there a red color in nature or are there different red colors?, A color is a tuple/list of numbers(in RGB is three colors) in a color 
model(the range of values you accept to describe a color, there is other than RGB, like HSV, etc) in a color space(the human eye color visible spectrum, this is what defines what red color
looks like). You can write RGB colors in HEX format, the 0 to 255 integers, or even floating point values. A chromaticity diagram shows what colors our eye can perceive, there is also 
imaginary colors(colors our eye can not percieve because their radio spectrum is out of our eye's capacity). Human eye is more sensitive to dark hues(dark colors), so if we would graphic
the colors RGB can represent you will find most colors near black and very few in the brighter hues side. there is some other color spaces, again the color space is the possible colors
the model accepts, for example AdobeRGB space area is bigger than RGB. and ProPhooRGB's space are is even bigger. To control pixels we use high level primitives like BItmap or Canvas, 
Bitmaps AKA Image, they are a type of raster image, in android we have the picture which is similar to a bitmap but it is actually a list of commands on the Canvas. Android used to render
all its UI using bitmaps, so things like a button view(in XML) was a bitmap, text is a special case but in theory they're also bitmaps but they're not really. There is different bitmap formats
JPEG< PNG, WebP, GIF, TIFF, in Android 12 it started supponting AVIF. BTW RGB only needs 3 bytes but it always store 4 bytes because it helps with memory alignment and this makes algorithms
more simple. Again, there is different formats, it could be stored as a BMP(bitmap) which is basically an images raw data, in a 100 by 100 image it would be 40KB, this is because 100X100x4, remember
4 is the space needed for an rgb color, Jpeg would be only 4k, and a gif would be only 156Bytes and PNG would be 1KB, PNG is good at changing in pixel color from one color to another, 
but it is bad at drawing picture but PNG efficiency could vary depending on the image we need to represent, GIFs could actually need more memory than some other image formats in some instances,
again, it all depends on the characteristics of the image. the color, color changes it is made from. Some of their diferences are

* Jepg lets you choose how much you want to spend on disk versus the quality of image but you can not use translucency/alpha, it offers different levels of "lossines"
* Jpeg Is opaque only, again, can't use translucency/alpha
* GIF offers 1-bit transparency
* GIF is limited to 256 colors(8 bits)
* PNG offers full translucency("alpha") but it is a lossless format, so it's always going to be slightly bigger, specially photos
* WebP offers more compression, you can choose between Lossy or Lossless and supports features like animation, alpha, etc
* AVIF can do HDR, they can encode over 10 or 12 bit of color depth, for more precision and color information

You choose your format based on the following characteristics

* Lossines
* Detail
* Color Information
* Translucency/Transparency
* Size
* Animation

**Files Size != Loaded Size**
For example when using a 3D renderer and loading some textures that are 4KB PNGs of gray color, but suppose their size is 4000x4000 gray PNGs, so they are only 4KB on disk space but when something like that 
is expanded on RAM, it would use around 68MB or RAM. In Android we can get the exact amount of Bytes of RAM an image is using with the following code

```
var sq_sm: Bitmap = BitmapFactory.decodeResource(resources, R.drawable.whitesquare_small)
println("Small: , h, bytes = ${sq_sm.width}, ${sq_sm.height}, ${sq_sm.allocationByteCount}")
```

A small image in any format that is small in disk space doesn't mean it will be small in RAM when loaded 







