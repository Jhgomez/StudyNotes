# Tesing
* [lincheck](https://kotlinlang.org/docs/lincheck-guide.html): This library could be used for testing corroutines
* **Turbine**: Also for testing corroutines, you can use Turbine, a cashapp library, according to marcin moscala [at 1h53m](https://youtu.be/mB6cJAXxFGk?si=Dy5aI997YkEoJKRu) you could replace the functionality of turbine with a few lines of
  code, essentially you could replace it by using the onEach flow operator and inside it collect every result of success in a collection and also a catch that is adding to a collection of
  failure and launch it in a background scope in the virtual runtime, but it’s hard because you need to advance time instead of awaiting items and check what is there. Turbine provides a
  way to decouple the flow emitter from your test in a way that makes possible to look at the structure of the output, await new elements,  check your flow meets conditions like if it is
  an empty flow, or make sure the flow only produces a certain number of elements, it basically sets you up with a lot of good defaults for collecting a flow elements.
