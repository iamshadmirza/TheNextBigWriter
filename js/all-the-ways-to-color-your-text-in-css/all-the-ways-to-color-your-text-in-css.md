Color property in CSS is a very common one. It is used whenever there is a need to provide different colors to Text. There are many ways to provide value to this property. Let's have a look into all those ways.

#### 1. Color Names

The simple and common way is through color names like red, green, blue, orange etc. There are total 140 color names in HTML and CSS color specification.

Some of the common color names:

> red, orange, blue, cyan, aqua

```css
h1 {
    color: orange;
}
```

> <h6 style="color:orange">I'm Orange</h6>
> <h6 style="color:red">I'm Red</h6>
> <h6 style="color:blue">I'm Blue</h6>
> <h6 style="color:seagreen">I'm Sea Green</h6>

These names are easy to remember as compared to other values for color property. All these color values represents the plain solid colors without any transparency.

#### 2. Hexadecimal Values

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

> <h3 style="color: #ff0000">I am completely opaque<h3>

```css
// semi-transparent color
h1 {
    color: #FF000080;
}
```

> <h3 style="color: #FF000080">I am semi-transparent<>

📌 **Browser Compatibility**

The browser support for #RRGGBBAA hex codes is great. IE doesn’t support it but otherwise you should be covered. Check [Can I Use](https://caniuse.com/#feat=css-rrggbbaa) for details if you’re curious.

#### 3. RGB Values

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
    color: rgba (0, 0, 255, 1);
}
```

> <h3 style="color: rgba(0, 0, 255, 1)">I am fully opaque<h3>

```css
// rgba value with transparency
h1 {
    color: rgba (0, 0, 255, 0.3);
}
```

> <h3 style="color: rgba(0, 0, 255, 0.3)">I am semi-transparent</h3>

📌 **Browser Compatibility**

The browser support for rgba() is great. Check [Can I Use](https://caniuse.com/#feat=rgba) for details if you’re curious.

#### 4. HSL / HSLA Values

HSL stands for hue, saturation, and lightness which is extended with an alpha value to be HSLA. It represents a cylindrical-coordinate representation of colors. This looks syntactically similar to rgb values but the ranges are different. An HSL / HSLA color value is specified with the hsl( ) / hsla( ) function, which has the following syntax:

> hsl (hue, saturation, lightness)

> hsla (hue, saturation, lightness, alpha)

**Hue**: Think of a color wheel. Around 0 and 360 degrees are reds. 120 degree is where greens are and 240 degree are blues. Use anything in between 0-360. Values above and below will be modulus 360.
**Saturation**: 0% is completely desaturated (grayscale). 100% is fully saturated (full color).
**Lightness**: 0% is completely dark (black). 100% is completely light (white). 50% is average lightness.
**alpha**: Opacity/Transparency value. 0 is fully transparent. 1 is fully opaque. 0.5 is 50% transparent.

```text
// hsl values - different shades of green

Green: hsl(120, 100%, 50%)
Light Green: hsl(120, 100%, 75%)
Pastel Green: hsl(120, 60%, 70%)
```

```css
// hsla value to provide full opacity

h1 {
    color: hsla(120, 100%, 50%, 1);
}
```

> <h3 style="color: hsla(120, 100%, 50%, 1)">I am fully opaque<h3>

```css
// hsla value with 50% transparency

h1 {
    color: hsla(120, 100%, 50%, 0.5);
}
```

> <h3 style="color: hsla(120, 100%, 50%, 0.5)">I am semi-transparent</h3>

📌 **Browser Compatibility**

The browser support for hsl( ) and hsla( ) is great. Check [Can I Use](https://caniuse.com/#feat=hsla) for details if you’re curious.

### No-Comma Color Functions in CSS

If you have noticed, that every single color function actually needs two functions, one for transparency and one without transparency. There is a new syntax which eliminates the need for having 2 functions.This new syntax eliminates the commas between each values in the function.

```css
/* New Syntax */
rgb(0 128 255)

rgb(0 128 255 / 50%)

hsl(198deg 28% 50%)

hsl(198deg 28% 50% / 50%)
```

📌 **Browser Compatibility**

The browser support is pretty good everything except IE11. Please do check [Can I Use](https://caniuse.com/#feat=mdn-css_types_color_space_separated_functional_notation) for details.

### New Color functions

The [CSS Color Module Level 4](https://www.w3.org/TR/css-color-4/) has few new color functions e.g. lab( ), lch( ) & [color ( )](https://alligator.io/css/color-function/). All these function will accept the new syntax described above. 



### Which One to Choose? :thinking:

As there are many options to provide color values, it's a tough decision to choose the one. Based on my experience I would explain certain points for each syntax, which can help to find out the right syntax as per the use-case.

**Color Names**: Different browsers have their own idea for a particular named color. So, you may find differences how a color [[aquamarine]] looks in different browsers.

**Hex Codes & RGB Values**: They both comes under a machine readbale format, which is not easy to understand by a dev. If you want to provide a lightness or darkness to a color you cannot provide it without changing the complete color code for both formats.

**HSL/HSLA Values**: It is an intuitive colour format that mimics the real world.I would like to explain it more with an example:

For example, you're probably sitting at a desk right now. Notice the colour of the desk. Let's say its a mahogany desk. It's colour values would be—

>Hex: #4f2017;
RGB: rgb(79, 32, 23);
HSL: hsl(10, 55%, 20%);

Now hold your hand above it, like a couple of inches above the surface. Your hand's shadow now makes the desktop a bit darker, right? Now, it's impossible to represent this colour change in hex or rgb, without changing the colour itself. But in hsl, it's a absolute easy- simply decrease the Lightness value, and bam! The colour remains the same, but with a bit of black mixed in— basically lessen the Lightness value.

>Hex: #4f2017; --------------> #200d09;
RGB: rgb(79, 32, 23); ------> rgb(32, 13, 9);
HSL: hsl(10, 55%, 20%); ----> hsl(10, 55%, 8%);

As you can see, the values of Hex and RGB have completely changed, whereas in HSL only one aspect has changed. Because of this, it becomes intuitively easy to create colour schemes on the fly.

So, my recommendation would be to use hsl a lot because getting accent colors from base color is very easy.

### Where else these values can be used?

Not only with color property, these values are also used with other css properties like **background-color**, **border-color**, **caret-color**, **text-decoration-color**, **outline-color**, **box-shadow**, **linear-gradient**.

-----

That’s all for now for this article. I have tried to share my knowledge, hoping to help others. Please comment your valuable suggestions and feedback.

[Dev.to](https://dev.to/mishraasoumyaa) | [Twitter](https://twitter.com/mishraaSoumya)
