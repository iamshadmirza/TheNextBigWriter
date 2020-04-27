Color property in css is a very common property. It is used whenever there is a need to provide different color to Text. There are many ways to provide values to this property. Let's have a look into all those ways.

#### 1. Hexadecimal Values

The word **hexadecimal** refers to a numerical value that uses 16 as a base instead of 10. A hexadecimal value can have 16 values for each digit in a number:

> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F

A hexadecimal color code is a combination of [[Red]], [[Green]], [[Blue]] & [[Alpha]] (optional) values. The most common format of the hex code is a 3 or 6 digit color code prefixed with **#**, which is followed by color codes for Red, Green and Blue [[#RRGGBB]]. The code for each of the color is a 2 digit hexadecimal number between [[0-9]] and ([[a-f or A-F]]).

For example, these all are valid hexadecimal values:

> 00, 0A, 1D, 9D, F5, 99, E4, CC

The 2 digit hexadecimal number for each color is combined to create a 6 digit color value. If both the digit for each color code is same, then the 6 digit color code can be written as a 3 digit color code.

```css
// valid color codes

#000000 or #000
#FFFFFF or #FFF or #fff or #ffffff
#FF0000 or #ff0000
#2962ff
```

📌 **#RRGGBBAA**

We can also change the transparency of a color with the hexadecimal value, just by adding the optional alpha value code [[AA]] in [[#RRGGBB]] to make it [[#RRGGBBAA]].
The AA value in #RRGGBBAA can range from the lowest value possible (00) to the highest value possible (FF). The lowest will make the color fully transparent, which means you won’t see it anymore. The highest value will make it completely opaque, which is the default for hex codes anyway.

```css
// color value with no alpha or fully opaque
h1 {
    color: #FF0000;
}
```

> <h3 style="color: #ff0000">I am completely opaque<h1>

```css
// semi-transparent color
h1 {
    color: #FF000080;
}
```

> <h3 style="color: #FF000080">I am semi-transparent<h1>

📌 **Browser Compatibility**

The browser support for #RRGGBBAA hex codes is great. IE doesn’t support it but otherwise you should be covered. Check [Can I Use](https://caniuse.com/#feat=css-rrggbbaa) for details if you’re curious.

#### 2. RGB Values

An RGB color values is specified with the [[rgb]] function which has the following syntax:

> rgb (red, green, blue)

The value for each color in the function defines the intensity of the color. Each color value is an integer between [[0 and 255]] or a percentage value from [[0% to 100%]].

For example, these all are valid rgb color values

```css
// valid rgb values

rgb (0, 0, 255)
rgb (0%, 0%, 100%)
rgb (0.5%, 3.5%, 0.5%)
rgb (89, 55, 255)
```

📌 **RGBA**

RGBA color values are an extension of RGB color values with an alpha value which provides opacity to the color similar to **#RRGGBBAA**. An RGBA color is specified with the [[rgba()]] function, which has the following syntax

> rgba (red, green, blue, alpha)

The alpha parameter in the above function is a number between 0.0 (fully transparent) and 1.0 (fully opaque).

```css
// rgba value to provide full opacity
h1 {
    color: rgba (255, 0, 0, 1);
}
```

> <h3 style="color: rgba(255, 0, 0, 1)">I am fully opaque<h3>

```css
// rgba value with transparency
h1 {
    color: rgba (255, 0, 0, 0.3);
}
```

> <h3 style="color: rgba(255, 0, 0, 0.3)">I am semi-transparent</h3>

📌 **Browser Compatibility**

The browser support for rgba() is great. Check [Can I Use](https://caniuse.com/#feat=rgba) for details if you’re curious.

#### 3. HSL Values

HSL stands for hue, saturation, and lightness - and represents a cylindrical-coordinate representation of colors. This looks syntactically similar to rgb values but the ranges are different. An HSL color value is specified with the hsl() function, which has the following syntax:

> hsl (hue, saturation, lightness)

**Hue**: Think of a color wheel. Around 0 and 360 degrees are reds. 120 degree is where greens are and 240 degree are blues. Use anything in between 0-360. Values above and below will be modulus 360.
**Saturation**: 0% is completely desaturated (grayscale). 100% is fully saturated (full color).
**Lightness**: 0% is completely dark (black). 100% is completely light (white). 50% is average lightness.
**alpha**: Opacity/Transparency value. 0 is fully transparent. 1 is fully opaque. 0.5 is 50% transparent.

```css
// valid hsl values - different shades of 

Green: hsl(120, 100%, 50%)
Light Green: hsl(120, 100%, 75%)
Pastel Green: hsl(120, 60%, 70%)
```

📌 **HSLA**

HSLA values are an extension of HSL values with an alpha value, which specifies the opacity of the color. An HSLA color value is specified with the hsla() function, which has the following syntax:

> hsla (hue, saturation, lightness, alpha)

The alpha parameter is a number between 0.0 (fully transparent) and 1.0 (fully opaque).

```css
// hsla value to provide full opacity

h1 {
    color: hsla(120, 100%, 50%, 1);
}
```

> <h3 style="color: hsla(120, 100%, 50%, 1)">I am fully opaque<h3>

```css
// hsla value with transparency

h1 {
    color: hsla(120, 100%, 50%, 0.5);
}
```

> <h3 style="color: hsla(120, 100%, 50%, 0.5)">I am semi-transparent</h3>

📌 **Browser Compatibility**

The browser support for hsl() and hsla() is great. Check [Can I Use](https://caniuse.com/#feat=hsla) for details if you’re curious.
