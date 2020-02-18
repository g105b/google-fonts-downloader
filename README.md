Download woff2 files from Google Fonts and generate Sass to load them
=====================================================================

This script is created to solve some repetitive problems that I personally find myself doing every time I work with Google Fonts. Here are the reasons why I wrote this:

1. Firstly, I prefer to ship my font files with my projects, rather than rely on cross-origin font downloads.
2. Google Fonts uses advanced optimisation techniques to offer the most efficient font files.
3. Working with highly-optimised font CSS is tedious.

Usage
-----

`./download CSS_URI [FONT_PATH_PREFIX] [OUTPUT_TO]`

* CSS_URI (required) - the URI provided from Google Fonts.
* FONT_PATH_PREFIX (optional, defaults to `/font`).
* OUTPUT_TO (optional, defaults to `{current-directory}/font`).

### Step by step:

1. Find a font (or fonts) you like at https://fonts.google.com, selecting the weights and styles you want.
2. Copy the embed URI. Example: `https://fonts.googleapis.com/css?family=Akronim|Fira+Sans:100,400,400i,700|Lacquer|Odibee+Sans&display=swap` 
3. Paste the embed URI as the first quoted parameter to this script: `./download "https://fonts.googleapis.com/css?family=Akronim|Fira+Sans:100,400,400i,700|Lacquer|Odibee+Sans&display=swap"`
4. Your woff2 files will be downloaded with sensible names alongside a Sass file that includes them all.

### End-to-end example:

```bash
git clone https://github.com/g105b/google-fonts-downloader
cd google-fonts-downloader
./download "https://fonts.googleapis.com/css?family=Akronim|Fira+Sans:100,400,400i,700|Lacquer|Odibee+Sans&display=swap" /asset/font ../../MyProject/src/font
```

#### Check the files that have downloaded:
```bash
ls ../../MyProject/src/font
```

```bash
akronim-regular-normal-latin-ext.woff2
akronim-regular-normal-latin.woff2
akronim.scss
fira-sans-bold-normal-cyrillic-ext.woff2
fira-sans-bold-normal-cyrillic.woff2
fira-sans-bold-normal-greek-ext.woff2
fira-sans-bold-normal-greek.woff2
fira-sans-bold-normal-latin-ext.woff2
fira-sans-bold-normal-latin.woff2
fira-sans-bold-normal-vietnamese.woff2
fira-sans-regular-italic-cyrillic-ext.woff2
fira-sans-regular-italic-cyrillic.woff2
fira-sans-regular-italic-greek-ext.woff2
fira-sans-regular-italic-greek.woff2
fira-sans-regular-italic-latin-ext.woff2
fira-sans-regular-italic-latin.woff2
fira-sans-regular-italic-vietnamese.woff2
fira-sans-regular-normal-cyrillic-ext.woff2
fira-sans-regular-normal-cyrillic.woff2
fira-sans-regular-normal-greek-ext.woff2
fira-sans-regular-normal-greek.woff2
fira-sans-regular-normal-latin-ext.woff2
fira-sans-regular-normal-latin.woff2
fira-sans-regular-normal-vietnamese.woff2
fira-sans.scss
fira-sans-thin-normal-cyrillic-ext.woff2
fira-sans-thin-normal-cyrillic.woff2
fira-sans-thin-normal-greek-ext.woff2
fira-sans-thin-normal-greek.woff2
fira-sans-thin-normal-latin-ext.woff2
fira-sans-thin-normal-latin.woff2
fira-sans-thin-normal-vietnamese.woff2
lacquer-regular-normal-latin.woff2
lacquer.scss
odibee-sans-regular-normal-latin.woff2
odibee-sans.scss
```

#### Check the contents of one of the generated scss files:
```bash
cat ../../MyProject/src/font/fira-sans.scss
```

```scss
$font-unicode-ranges: (
	cyrillic-ext: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F",
	cyrillic: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116",
	greek-ext: "U+1F00-1FFF",
	greek: "U+0370-03FF",
	vietnamese: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB",
	latin-ext: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF",
	latin: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD",
);

$font-styles: 
	italic
	normal
;
$font-weights: (
	regular: 400,
	thin: 100,
	bold: 700,
);

@each $unicode-name, $unicode-range in $font-unicode-ranges {
	@each $style in $font-styles {
		@each $weight-name, $weight-value in $font-weights {
			@font-face {
				font-family: "Roboto Slab";
				font-style: $style;
				font-weight: $weight-value;
				font-display: swap;
				src: url("/asset/font/fira-sans-#{$weight-name}-#{$style}-#{$unicode-name}.woff2") format("woff2");
				unicode-range: $unicode-range;
			}
		}
	}
}
```

#### Finally, see how this renders as CSS:

```bash
sass ../../MyProject/src/font/fira-sans.scss
```

```css
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-cyrillic-ext.woff2") format("woff2");
  unicode-range: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-cyrillic-ext.woff2") format("woff2");
  unicode-range: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-cyrillic-ext.woff2") format("woff2");
  unicode-range: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-cyrillic-ext.woff2") format("woff2");
  unicode-range: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-cyrillic-ext.woff2") format("woff2");
  unicode-range: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-cyrillic-ext.woff2") format("woff2");
  unicode-range: "U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-cyrillic.woff2") format("woff2");
  unicode-range: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-cyrillic.woff2") format("woff2");
  unicode-range: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-cyrillic.woff2") format("woff2");
  unicode-range: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-cyrillic.woff2") format("woff2");
  unicode-range: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-cyrillic.woff2") format("woff2");
  unicode-range: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-cyrillic.woff2") format("woff2");
  unicode-range: "U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-greek-ext.woff2") format("woff2");
  unicode-range: "U+1F00-1FFF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-greek-ext.woff2") format("woff2");
  unicode-range: "U+1F00-1FFF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-greek-ext.woff2") format("woff2");
  unicode-range: "U+1F00-1FFF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-greek-ext.woff2") format("woff2");
  unicode-range: "U+1F00-1FFF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-greek-ext.woff2") format("woff2");
  unicode-range: "U+1F00-1FFF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-greek-ext.woff2") format("woff2");
  unicode-range: "U+1F00-1FFF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-greek.woff2") format("woff2");
  unicode-range: "U+0370-03FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-greek.woff2") format("woff2");
  unicode-range: "U+0370-03FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-greek.woff2") format("woff2");
  unicode-range: "U+0370-03FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-greek.woff2") format("woff2");
  unicode-range: "U+0370-03FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-greek.woff2") format("woff2");
  unicode-range: "U+0370-03FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-greek.woff2") format("woff2");
  unicode-range: "U+0370-03FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-vietnamese.woff2") format("woff2");
  unicode-range: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-vietnamese.woff2") format("woff2");
  unicode-range: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-vietnamese.woff2") format("woff2");
  unicode-range: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-vietnamese.woff2") format("woff2");
  unicode-range: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-vietnamese.woff2") format("woff2");
  unicode-range: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-vietnamese.woff2") format("woff2");
  unicode-range: "U+0102-0103, U+0110-0111, U+0128-0129, U+0168-0169, U+01A0-01A1, U+01AF-01B0, U+1EA0-1EF9, U+20AB"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-latin-ext.woff2") format("woff2");
  unicode-range: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-latin-ext.woff2") format("woff2");
  unicode-range: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-latin-ext.woff2") format("woff2");
  unicode-range: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-latin-ext.woff2") format("woff2");
  unicode-range: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-latin-ext.woff2") format("woff2");
  unicode-range: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-latin-ext.woff2") format("woff2");
  unicode-range: "U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-italic-latin.woff2") format("woff2");
  unicode-range: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-italic-latin.woff2") format("woff2");
  unicode-range: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: italic;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-italic-latin.woff2") format("woff2");
  unicode-range: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("/asset/font/fira-sans-regular-normal-latin.woff2") format("woff2");
  unicode-range: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 100;
  font-display: swap;
  src: url("/asset/font/fira-sans-thin-normal-latin.woff2") format("woff2");
  unicode-range: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD"; }
@font-face {
  font-family: "Roboto Slab";
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url("/asset/font/fira-sans-bold-normal-latin.woff2") format("woff2");
  unicode-range: "U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD"; }
```