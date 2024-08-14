* For **rendering** Android it uses SKIA for other targets it uses SKIKO

* **Modifier.onPreviewKeyEvent** used when targeting desktop to capture key presses

* The android extension API called **Pallete** help us extract color information from a bitmap and a library called **kmpPallete** lets us extract other pallete info like dominant color and vibrant color from a bitmap

* **Modifier.graphicsLayer** helps us manipulate the size and placement original values, generated in the layout phase, of the composable and it only affects the drawing phase, we can even use this modifier to "draw" the composable outside of the screen bounds