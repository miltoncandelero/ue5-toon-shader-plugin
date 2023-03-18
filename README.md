# Unreal Engine 5 Toon Shader
## [by Christopher Sims](https://twitter.com/csims314/status/1412863101196713993)

### The following is lifted from Christopher's twitter.

UE5 Lumen and Nanite compatible toon shader. 3 methods for cel shading, 7 methods for outlines, and a custom function example. 

https://user-images.githubusercontent.com/15253010/226077619-33c4f627-3954-4262-99fd-311043e39a8f.mp4

---

This is an unlit surface shader. The diffuse and specular colors are based on the main directional light in the scene. Very consistent results, but we can do more...

![E5t7J9wWUAQhqmo](https://user-images.githubusercontent.com/15253010/226077700-cbd82c83-5713-4b94-9843-4b5b30637e05.jpg)

---

Desaturate the final render, mask out the shadow and change it’s color to match the cel shading bands

![E5t7TFnWUAEu1mO](https://user-images.githubusercontent.com/15253010/226077777-2963840e-64ce-4f96-8360-b20ab8d5fe3c.jpg)

---

Desaturate the entire scene and posterize the result. You get really noisy edges because Lumen is raytracing, but it’s still a neat style.

![E5t7bH1X0AQtnzK](https://user-images.githubusercontent.com/15253010/226077825-58cd23b9-9537-4753-b132-827f90b756ec.jpg)

---

As of UE 4.2 you can do a separate render pass for just the transparent objects in your scene. Then apply any edge detection algorithm you’d like. Looks awesome with animated fractures

![E5t7kw_XIAsLhrb](https://user-images.githubusercontent.com/15253010/226077851-5e76236f-6520-4a00-8510-24226fd73020.jpg)

---

If you turn indirect lighting intensity all the way down, Lumen shadows become crisp enough to do a nice comic style outline around the shadows


![E5t7xDHXoAECrir](https://user-images.githubusercontent.com/15253010/226077891-38c4efd8-bd6d-49b2-bf96-18b7997a773b.jpg)

---

For Depth based edges, the edges fade fhe further away from the camera and rather than use a hard threshold, a multiplier and bias is used

![E5t73BrXIAg5O6p](https://user-images.githubusercontent.com/15253010/226077945-d9b284d7-9fe5-4bbd-a330-85f67655c6ad.jpg)

---

Normals edge detection is a great complement to depth edges because you can catch edges within each object like on the cube

![E5t79HfXIAUULqh](https://user-images.githubusercontent.com/15253010/226077976-74de9dcc-d4d7-4ff4-859f-85ccb5215f2f.jpg)

---

This is a nice method when you want edges everywhere and you don’t want to fiddle with sensitivity settings

![E5t8CroX0A0JwrZ](https://user-images.githubusercontent.com/15253010/226078020-77d05486-a677-4de0-ba68-78daf239dc70.jpg)

---

Stick a texture into the specular channel of the surface shader, then sample it in post and overlay the edges on the final render

![E5t8ILyXwAAjsaW](https://user-images.githubusercontent.com/15253010/226078174-55b70f97-0c60-405a-b3b5-0cc679d79c19.jpg)

---

During modeling, or using the UE Modeling plugin, assign a random value to the red channel of each faces vertex color, and again feed it into the specular channel for edge detection

![E5t8Ra5XIAgR_ht](https://user-images.githubusercontent.com/15253010/226078214-340929b3-8b54-40ed-8d07-3e79ab9d7d06.jpg)

---

A pseudo random number based on each object’s WS position, and again use that value in the specular channel. It’s much faster than manually coloring vertices

![E5t8cl5WEAUn603](https://user-images.githubusercontent.com/15253010/226078253-f4db9afb-5fcd-46de-acc6-d4e009d3009e.jpg)

---

Nanite does not support a custom depth buffer yet so use a specular value of 0 to disable normal based outlines in post, and a range of .1 - .5 for everything else, in particular object position color. Low specular values are imperceptible

![E5t8jzXXEAIK1nZ](https://user-images.githubusercontent.com/15253010/226078334-ee81c899-fff4-402c-b3bf-9b9f31e76491.png)

---

The custom function material node allows you to do loops so you can achieve Voronoi patterns, among others. 

![E5t8pEFXEAIH-To](https://user-images.githubusercontent.com/15253010/226078378-a22fc8b5-3f7f-44f1-adca-47d6f80a3c95.jpg)

