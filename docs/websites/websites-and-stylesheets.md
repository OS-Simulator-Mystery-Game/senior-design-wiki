### Page Markdown Guide

> Quick note: Make sure to go to your settings and add the file extensions! Go to Godot>Editor settings>Docks>FileSystem and add `.ntml` (to be changed) and `.sds` to the TextFile line. Don't include the dots, and make sure to separate the extensions by commas!

#### Tags/elements
The following tags are mandatory in any markup file, and are important in properly structuring the page:
- `<ntml>` (to be updated): Denotes the start of a new page file. Doesn't accept styling in its opening tag.
- `<head>`: Denotes the section of the document containing site metadata like the title, description, tags, page music, and stylesheet file location. Doesn't accept styling in its opening tag.
- `<body>`: Denotes the start of the page. Serves mainly as a background for the page's content. Contains `<page>`.
- `<page>`: Denotes the start of the page's actual content. Is a child of `<body>`.

The following tags are used for page elements and grouping:
- `<box>`: Creates a new **Content Box**. Helps with grouping items together.
- `<text>`: Creates a new block of text. Can be decorated with spans and links.
- `<list>`: Creates a new **List**. Display other page elements in a bulleted or ordered list!
- `<img>`: Creates a new **Image**. Allows visitors to view an image. Has a `destination` property in order to navigate to other pages.
- `<aud>`: Creates a new **Audio Player**. Allows visitors to listen to the specified audio file.
- `<vid>`: Creates a new **Video Player**. Allows visitors to view a video on the webpage.
- `<file>`: Creates a new **File Download**. Allows visitors to download the specified file.
- `<input>`: Creates a new **Input Element**. Can be changed to various input types with various parameters.
- `<embed>`: Creates a new **Embed**. Can be provided with an application file in order to load it within the webpage.
- `<span>`: Creates a new **Span**. Can be styled. Must be contained within a `<text>` tag.
- `<link>`: Creates a new **Link**. Can be styled, and has a `destination` property to navigate to another page. Must be contained within a `<text>` tag.

Grouping tags like `<ntml>`, `<head>`, `<body>`, `<page>`, `<box>`, and `<list>` are closed with the closing tag `</>`.
Text tags are closed with `</>`, and the `link`s/`span`s inbetween are closed with `</>` as well. Spans and links can only be used inside of `<text>` elements. Text between the opening and closing tag is rendered on the page.
All other tags close themselves, in the format `<[TAG] [PROPERTIES] />`.

> NOTE: Spans and links must have a specified `length` property that determines how many characters from their opening tag they style. You can also specify a `zindex` property to control how overlapping `span`s or `link`s interact.

#### Getting started
To create a new file, you need to start with the following document setup:

```
<ntml>
	<head>
		 title=""
		 info=""
		 tags=""
		 stylesheet=""
		 music=""
	</>
	<body>
		<page>
		</>
	</>
</>
```

From there, feel free to adjust the metadata in `<head>` and add child elements to `<page>`! Page files are saved with the extension `.ntml` (to be changed).

#### Element properties
Element properties are crucial to having a hip webpage! Properties can be added by simply adding them in the format `[PROPERTY_NAME]=[VALUE]` after the tag type in the opening tag. The following properties are able to be used for styling elements, with some affecting only particular elements.

General-purpose properties (some apply only to MOST elements; some won't apply for links and spans):

- `id`: Sets the ID of the page element. Later to be used in `Recipe`(`.ssr`) code files. Requires quotes around the ID, and must be unique to ensure intended behavior.
- `class`: Sets the base class for the page element. Requires quotes around the class name.
	- Cannot be set within a stylesheet.
- `hover`: Sets the class to be used for the element when it is hovered. Requires quotes around the class name.
	- Cannot be set within a stylesheet.
- `clicked`: Sets the class to be used for the element when it is clicked. Requires quotes around the class name.
	- Cannot be set within a stylesheet.
- `size`: Sets the size of the page element on the page. Specified by 2 non-negative integers followed by "px", with no spaces. (ex. `size=100px100px`)
- `position`: Sets the position of the element on the page, as well as the z-index of this element to define layering. Only works in `anchored` or `absolute` positioning modes. Specified by 3 non-negative integers followed by "px", with no spaces. (ex. `size=100px100px5px`)
- `display`: Determines how an image positions itself on a page. Set to `flow`, `anchored`, or `absolute`. `Anchored` elements move with the page, but are not automatically aligned inside of its parent. `Absolute` elements stay on the same position on the page no matter how it is scrolled by the user (good for navigation bars).
- `margin`: Sets the margins of this element. Specified by 4 non-negative integers followed by "px", with no spaces, with the first number correlating to the top margin, the second to the left margin, the third to the right margin, and the fourth to the bottom margin. (ex. `size=10px10px10px10px`)
- `padding`: Sets the padding of the element. Specified by 4 non-negative integers followed by "px", with no spaces, with the first number correlating to the top padding amount, the second to the left padding amount, the third to the right padding amount, and the fourth to the bottom padding amount. (ex. `size=10px10px10px10px`)
- `bg_color`: Sets the background color of the element. Set to a hex code prefixed by a `#` (quotes are not needed). Opacity is supported in the hex code by adding an additional 2 characters beyond the normal 6. (ex. #0fa4cf0f)
- `corner_size`: Sets the rounding radius of the corners of the element's background. Does not affect image backgrounds. Specified by 4 non-negative integers followed by "px", with no spaces, with the first number correlating to the top left corner radius, the second to the top right corner radius, the third to the bottom left corner radius, and the fourth to the bottom right corner radius. (ex. `size=10px10px10px10px`)
- `shadow`: Enables or disables a shadow effect on the element. Set to `true` or `false`.
- `shadow_color`: Sets the shadow color for the page element. Set to a hex code prefixed by a `#` (quotes are not needed). Opacity is supported in the hex code by adding an additional 2 characters beyond the normal 6. (ex. #0fa4cf0f)
- `shadow_size`: Sets the shadow size for the page element. Specified by a non-negative integer followed by "px".
- `shadow_offset`: Sets the shadow offset for the page element. Specified by 2 integers followed by "px", with no spaces. (ex. `size=100px100px`)
- `bg_image`: Specifies the path of the file to be used for the element. Set to a relative filepath surrounded by quotes. First, the site's directory is checked, and then the user's root directory is checked for the file.
- `bg_repeat`: Determines if an image stretches or tiles. Set to `tile` or `repeat`.
- `border_color`: Sets the border color for the page element. Set to a hex code prefixed by a `#` (quotes are not needed). Opacity is supported in the hex code by adding an additional 2 characters beyond the normal 6. (ex. #0fa4cf0f)
- `border_size`: Sets the thickness of the colored border for the page element. Set to a non-negative integer.
- `border_image`: Specifies the path of the file to be used for the element's border. Set to a relative filepath surrounded by quotes. First, the site's directory is checked, and then the user's root directory is checked for the file.
- `border_margins`: Specifies the thickness of the image border based on the source file provided, so it can stretch and size appropriately. Specified by 4 non-negative integers followed by "px", with no spaces, with the first number correlating to the top margin, the second to the left margin, the third to the right margin, and the fourth to the bottom margin. (ex. `size=10px10px10px10px`)

> Elements from this point on only affect certain element types.

- `alignment`: Determines how elements are laid out in a container element. Set to `begin`, `center`, or `end`.
	- Used on: Page Content, Content Boxes
- `direction`: Determines how elements are laid out in a container element. Set to `horizontal` or `vertical`.
	- Used on: Page Content, Content Boxes
- `text`: The default text for `text` elements to be set to. Set to a string surrounded by quotes.
	- Used on: Text blocks
- `font`: Sets the font of the `text` element, or the bullet font for `list` elements. Available fonts are: `times`, `philosopher`, `celtica`, `goblinhand`, `wizard`, `frankenstein`, `angelica`, `electrofied`, `unispace`, `shantell`, `comic`, and `default` (system font).
	- Used on: Text blocks, lists
- `font_size`: Sets the font size of `text` elements. Set to an integer greater than or equal to 0.
	- Used on: Text blocks, lists
- `color`: Sets the font color of the `text`, `list` bullets, `span`, or `link`. Set to a hex code prefixed by a `#` (quotes are not needed). Opacity is supported in the hex code by adding an additional 2 characters beyond the normal 6. (ex. #0fa4cf0f)
	- Used on: Text blocks, lists, spans, links
- `text_align`: Sets the alignment of the text inside `text` elements. Set to either `left`, `center`, or `right`.
	- Used on: Text blocks
- `text_shadow_color`: Sets the text shadow color of the `text` or `list` bullets. Set to a hex code prefixed by a `#` (quotes are not needed). Opacity is supported in the hex code by adding an additional 2 characters beyond the normal 6. (ex. #0fa4cf0f)
- `text_shadow_size`: Sets the shadow size of `text` elements. Set to an integer greater than or equal to 0. (good for outlines too!)
	- Used on: Text blocks, lists
- `text_shadow_offset`: Sets the shadow size of `text` and `list` elements. Specified by 2 integers followed by "px", with no spaces. (ex. `size=100px100px`)
	- Used on: Text blocks, lists
- `destination`: The URL to be loaded when an `image` or `link` element is clicked. Set to a string surrounded by quotes.
	- Used on: Images, links
- `file`: Specifies the path of the file to be used for the element. Set to a relative filepath surrounded by quotes. First, the site's directory is checked, and then the user's root directory is checked for the file.
	- Used on: Images, videos, audio players, file downloads, embedded content
- `mode`: Determines if an image stretches or tiles. Set to `tile` or `repeat`.
	- Used on: Images
- `frames`: The amount of frames the image contains. Set to an integer greater than or equal to 1. Used for animated images.
	- Used on: Images
- `speed`: The speed the animated image plays at. Set to a float greater than or equal to 0.0.
	- Used on: Images
- `flip_x`: Flips the image on the x-axis if `true`. Set to `true` or `false`.
	- Used on: Images
- `flip_y`: Flips the image on the y-axis if `true`. Set to `true` or `false`.
	- Used on: Images
- `autoplay`: Determines if the video plays as soon as it loads on the page. Set to `true` or `false`.
	- Used on: Videos
- `controls_enabled`: Determines if the visitor can scrub or adjust the volume of the video on the page. Set to `true` or `false`.
	- Used on: Videos
- `type`: Determines the type of input element. Set to `text`, `password`, `number`, `slider`, `checkbox`, `dropdown`, `upload`, or `button`.
	- Used on: Input
- `range`: Determines the maximum and minimum values of a slider's range. Specified by 2 non-negative integers followed by "px", with no spaces. (ex. `size=100px100px`)
	- Used on: Input (sliders)
- `prechecked`: Specifies if a "tickbox" `input` element is already checked or not. Set to `true` or `false`.
	- Used on: Input (tickboxes)
- `items`: Specifies the items displayed in a "dropdown" `input` element. Enter a string surrounded by quotes, with items separated by commas.
	- Used on: Input (dropdown)
- `label`: Specifies the text appearing on a "button" `input` element. Specified by a string.
	- Used on: Input (button)
- `disabled`: Specifies if a "button" `input` element can be pressed or not. Set to `true` or `false`.
	- Used on: Input (button)
- `ordered`: Specifies if the `list` element's bullets are ordered or not. Set to `true` or `false`.
	- Used on: Lists
- `horizontal_items`: Specifies the amount of horizontal elements to display in a `list` element. Specified by an integer greater than or equal to 1.
	- Used on: Lists
- `bold`: Makes the contained text bold (if the font supports it). Set to `true` or `false`.
	- Used on: Spans, links
- `italic`: Makes the contained text italic (if the font supports it). Set to `true` or `false`.
	- Used on: Spans, links
- `underline`: Applies an underline effect to the contained text. Set to `true` or `false`.
	- Used on: Spans, links
- `striked`: Applies a strikethrough effect to the contained text. Set to `true` or `false`.
	- Used on: Spans, links
- `shake`: Applies a shaking effect to the contained text. Set to `true` or `false`.
	- Used on: Spans, links
- `wave`: Applies a wave effect to the contained text. Set to `true` or `false`.
	- Used on: Spans, links
- `tornado`: Applies a tornado effect to the contained text. Set to `true` or `false`.
	- Used on: Spans, links
- `rainbow`: Applies a rainbow effect to the contained text. Set to `true` or `false`.
	- Used on: Spans, links
- `zindex`: The height of the `span` or `link` element that determines its layering on top of other `span`s or `link`s in the same `text` element. Set to a non-negative integer.
	- Used on: Spans, links
- `length`: The length of the `span` or `link` element from its opening tag. Set to a non-negative integer.
	- Used on: Spans, links

The following tags set page metadata in `<head>`:

- `title`: The title of this page.
- `info`: A description of this page. Contained in quotes.
- `tags`: A comma-separated list of tags for this webpage. Contained in quotes.
- `stylesheet`: The relative path to this page's stylesheet from the site's base directory. Contained in quotes.
- `music`: The ID of the music to be played on this website. Contained in quotes.

> NOTE: When entering strings, make sure to escape special characters like `<` and `/`!

Sample elements:

```
<page bg_color=#c38b61ff>
	<text font_size=40px>Max's Website</>
	<box bg_color=#eeb585ff>
		<text font=philosopher>This is my marginally bigger textbox.</>
		<text font=philosopher font_size=12px>Another set of words!</>
	</>
	<img file="desktop/dr_gerber.viz" size=409px409px/>
</>
```

### Stylesheet Markdown

#### Formatting classes
Classes are easy to make with DecoScript! You can make one in the following format:

```
<class="\[YOUR CLASS NAME HERE]\">
    [properties here]
</>
```

Properties inside of classes are specified in the following format:

```<[PROPERTY_NAME]=[VALUE]>```

You can include as many classes as you want, and properties that apply to different kinds of elements can be applied in the same class safely!

Class files are saved with the extension `.sds`.

Sample stylesheet:
```
<class="hello">
	<color=#ffffff>
</>

<class="ooooooh">
	<color=#ff0000>
</>

<class="normal">
	<color=#ffff00>
</>

<class="wave">
	<wave=true>
</>
```