Color property in css is a very common property. It is used whenever there is a need to provide different color to Text. There are many ways to provide values to this property. Let's have a look into all those ways.

#### Hexadecimal Values

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
