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

A small image in any format that is small in disk space doesn't mean it will be small in RAM when loaded.

So what can we do? only load the bits you need, only load the size you need. Use resource qualifiers, for example if you put an image on the drawable resource folder, when the system loads it, it will upscale
it automatically, so for example if you put an image in that folder and load it in a moder device, that image will upscale around 4(could be more in moder devices) times its on each axis, so it will require
16 times more memory space, so if you put an HD image in there you could stress the memory of the phone, so that is why you use resource qualifiers, you could use the `drawable-nodpi` resource qualifier as
resources in that folder wont be scaled at all. You should also keep only necessary bitmaps around and reuse bitmap, you do that by using a good bitmap cache like Coil.

In Android you draw bitmaps directly with `Canvas.drawBitmap()` function, or indirectly by instantiating a `BitmapDrawable` and pass it as a background of a view.

Text are bitmaps but their rendering pipeline involves actually transforming them from vector information obtained in the font file, the font file contains vector information, these vectors are also known as
"glyphs", the obtained bitmaps are then copied to the screen, this is done by a C library that Android uses called `FreeTypeRenderer`, it receives vector info and transforms it into bitmaps that are then drawn
into a cache known as `GlyphCache`, this cache can be thought as a big canvas and the system knows where on it a character lives, and if a character has been cache before, it will return the same character
instead of creating a new one.

## Bitmap Scaling
They up-scale and down-scale somewhat poorly, not greatly. 

## Bitmap Filtering
There is several bitmap/pixel filtering methods/approaches/techniques, but android supports two. There is two operands in filtering calculations, source and destination. One is, point-sampled/point/pixel
filtering, here the destination pixels color values are used to find the most similar pixels in the source and those are filtered in, all other colors in the source pixels are dropped. THe other is, 
Bilinear filtering, here we the pixels around the pixels we need are used to calculate an average so the information persist in the form of an average, so in point filtering you lose information while in 
bilinear filtering it is transformed but not lost

## NinePatch Images(N-Patch)
In Android these are used to be able to scale bitmaps/drawables correctly. But they are some work around, and what you actually would want is vectors.

## Vectors
They are canvas commands instead of pixel information. You can think of it mostly like `Canvas.drawPath()`, but also `Canvas.drawLine()`. When you draw a rounder rectangle or circle Android mostlikely will 
ask the system to draw a path instead of using specific code drawing different shapes. `VectorDrawable`s are a set of canvas commands, from painting to path, we also have access to do transforms, gradients, matrix.

Lottie is a library that lets you parse complex adobe after effects vector animations which are exported as json files with bodymotion

## Types of fills in Paths
So Paths objects rendered in Canvas are Vector graphics, there is two types of fill modes for paths, there is Non-zero and even-odd. In Even-odd imagine a star drawn inside a circle for
example, for every row of pixels we should create a counter that starts at zero and we should walk the lines of pixels from left to right, btw, these lines are the physical screen rows of
pixels, as soon as we find an intersection we should increase the counter by one, and when is 1 the counter is odd, and this tells us we are inside the path(inside the circle), so we should
start filling the path, in the next intersection the counter is 2, is even, so we stop drawing/painting the fill, and after going through every row of pixels in the screen we will end up with 
t he inner space of the path filled with the specified color. The other mode is Non-zero, it takes into account the winding of a path, in the same path example, the winding is the order in 
which you've defined the points(the pixels of the path). So suppose the circle starts at 90 degrees angle, and its order is clock wise, the star is the same, the initial point is at a corner
of the star that is also at the same X axis value as the circle starting point and with a Y axis value that is inside the circle, and it also draws its points in the same direction(clock-wise)
now we are supposed to do go by pixel rows again, when we find the first point of the circle from left to right we check what would be the next pixel and if it is considered a point forward
the current position instead of a previous point then we add one, the next point in the row would be a start path point, the next point is forward so we add one, now counter is two, next pixel
in a path also belongs to the star but its next point value is lower than the last point we were in so that is considered "backwards" direction, so we subtract one, now our counter is one, the
next pixel in a path is a cirlce's path pixel, but its next pixel relative to the current pixel being evaluated is also a lower value than the last pixel of the circle we evaluated so we 
subtract one, now our path is zero, in this method every time the counter is not zero we draw the color, that means we fill its content with the requested color, but if you think abour it,
if we do this our star content is also filled with the requested color resulting in a circle filled with the requested color, but it shouldn't fill the star content, the solution to this is 
change the direction of the points of the paths, if a path is inside another path and you don't want those filled then you need to have the inner path pixels have an opossite direction.

Stroke width is just a convenience, this is true because what happens under the hood when you request a stroke for a cirlce of radio X and stroke width of Y, then the stroke is created by 
drawing a circle with radio of X + Y and filling the space betwwen those two circles with the color you requested, but you could do this yourself so that is wht it is said is just a 
convenience method















