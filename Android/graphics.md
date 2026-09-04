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
