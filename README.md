# Sass Mix

**Library of useful sass mixins**

## Blending functions
These functions attempt to support the color blending Photoshop provides.
All functions expect a color as the `$foreground` and `$background` colors. The colors can be any hex, [rgb](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#rgb-instance_method), [rgba](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#rgba-instance_method), [hsl](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#hsl-instance_method), or [hsla](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#hsla-instance_method) color supported by Sass. Blending functions work by combining the colors from the top-most layer, the `$foreground`, with the lower layer, the `$background`.

**NOTE:** All blending and HSV functions were taken directly from [scss-blend-modes](https://github.com/heygrady/scss-blend-modes), namespaced under `mix-`, and reordered to work without compass support.

- **mix-blend-normal(** *$foreground*, *$background* **)** - Normal is used primarily to preserve the opacity after the blending has been applied to the RGB values.
- **mix-blend-multiply(** *$foreground*, *$background* **)**
- **mix-blend-lighten(** *$foreground*, *$background* **)**
- **mix-blend-darken(** *$foreground*, *$background* **)**
- **mix-blend-darkercolor(** *$foreground*, *$background* **)** - Not found in Photoshop.
- **mix-blend-lightercolor(** *$foreground*, *$background* **)** - Not found in Photoshop.
- **mix-blend-lineardodge(** *$foreground*, *$background* **)**
- **mix-blend-linearburn(** *$foreground*, *$background* **)**
- **mix-blend-difference(** *$foreground*, *$background* **)**
- **mix-blend-screen(** *$foreground*, *$background* **)**
- **mix-blend-exclusion(** *$foreground*, *$background* **)**
- **mix-blend-overlay(** *$foreground*, *$background* **)**
- **mix-blend-softlight(** *$foreground*, *$background* **)**
- **mix-blend-hardlight(** *$foreground*, *$background* **)**
- **mix-blend-colordodge(** *$foreground*, *$background* **)**
- **mix-blend-colorburn(** *$foreground*, *$background* **)**
- **mix-blend-linearlight(** *$foreground*, *$background* **)**
- **mix-blend-vividlight(** *$foreground*, *$background* **)**
- **mix-blend-pinlight(** *$foreground*, *$background* **)**
- **mix-blend-hardmix(** *$foreground*, *$background* **)**
- **mix-blend-colorblend(** *$foreground*, *$background* **)**
- **mix-blend-dissolve(** *$foreground*, *$background* **)** - Not implemented. Dissolve treats transparency as a pixel pattern and applies a diffusion dither pattern.
- **mix-blend-divide(** *$foreground*, *$background* **)**
- **mix-blend-hue(** *$foreground*, *$background* **)**
- **mix-blend-luminosity(** *$foreground*, *$background* **)**
- **mix-blend-saturation(** *$foreground*, *$background* **)**
- **mix-blend-subtract(** *$foreground*, *$background* **)**

### Examples

```scss
// Solid background
.multiply {
	background-color: blend-multiply(#7FFFD4, #DEB887);
}

// RGBa background
.multiply {
	background-color: blend-multiply(rgba(#7FFFD4, 0.5), rgba(#DEB887, 0.5));
}
```

## HSV Functions
These functions are used to convert between RGB, HSL and HSV color formats. The HSV color format is not natively supported by CSS or Sass. These functions were taken directly from this [Gist](https://gist.github.com/1069204). HSV values are used to calculate the results for the `mix-blend-colorblend`, `mix-blend-hue`, `mix-blend-luminosity` and `mix-blend-saturation` functions.

**NOTE:** As above, these are from [scss-blend-modes](https://github.com/heygrady/scss-blend-modes).

- **mix-hsv-to-hsl(** *$h*, [ *$s: 0*, *$v: 0* ] **)** - Converts a HSV color values into HSL color values. `$h` can be a list of three values representing `$h`, `$s` and `$v`.
- **mix-hsl-to-hsv(** *$h*, [ *$ss: 0*, *$ll: 0* ] **)** - Converts a HSL color values into HSV color values. `$h` can be a list of three values representing `$h`, `$ss` and `$ll`.
- **mix-color-to-hsv(** *$color* **)** - Converts a [Sass Color](http://sass-lang.com/docs/yardoc/Sass/Script/Color.html) into a [list](http://sass-lang.com/docs/yardoc/Sass/Script/List.html) HSV color values.
- **mix-hsv-to-color(** *$h*, [ *$s: 0*, *$v: 0* ] **)** - Converts a list of HSV color values into a Sass Color. `$h` can be a list of three values representing `$h`, `$s` and `$v`

## Center
Center transform an element on an axis. Doesn't include position absolute.
 
### Example

```scss
.container {
    position: relative;
    height: 500px;
    width: 500px;

    .centered {
	    position: absolute;
	    @include mix-center;
	}
}
```

## Clearfix
Clearfix an element containing floats.
 
### Example

```scss
.container {
    @include mix-clearfix;

    .float-left {
	    float: left;
	}
	
	.float-right {
        float: right;
    }
}
```

## Pick Visible Color
Returns the most visible colour for a given background.
 
### Example

```scss
.panel__heading {
    color: mix-pick-visible-color($background-color, $black-text-color, $white-text-color);
}
```

## Tint and Shade
Alternative to sass lighten and darken. Tint is a mix of color with white, shade is a mix of color with black.
 
### Example

```scss
.background {
    background-color: tint(red, 40%);
}

.background {
    background-color: shade(blue, 60%);
}
```

## Ellipsis
Truncate text and add an ellipsis
 
### Example

```scss
.panel__heading {
    @include mix-ellipsis(90%);
}

.panel__heading {
    // Defaults to 100%
    @include mix-ellipsis;
}
```

## Viewport Units
Fix for vw, vh, vmin, vmax on iOS 7.
Works by replacing viewport units with px values on known screen sizes.
 
### Example

```scss
.banner {
    @include mix-viewport-unit(height, 50vh);
}
```

## HiDPI
Target high DPI devices.

**NOTE:** Default is 1.3 to target the Nexus 7. You can find more DPI ratios [here](https://bjango.com/articles/min-device-pixel-ratio).
 
### Example

```scss
.image {
    background-image: url(normal-dpi.png);

    @include hidpi(1.5) {
        background-image: url(high-dpi.png);
    }
}
```