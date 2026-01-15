# Project 1 README

Student 1: Maxwell Tran (924628021)

## Project Status
The project is complete:
- SVG functions are written and pass the tests in SVGTest.cpp
- 100% code coverage has been achieved for both lines and functions
- The generated svg file matches the given svg file
- Makefile requirements are met
- README document is filled out

## Known Issues
The total number of characters for each SVG tag must not exceed 199; otherwise, the buffer 
used in the SVG function for that tag will overflow. Therefore, the SVG functions
will return an error (SVG_ERR_INVALID_ARG) if the number of characters in the buffer
is greater than or equal to 200.

## Code References
* [GoogleTest User's Guide](https://google.github.io/googletest/)

## Generative AI Use
I used Claude for Prompt 1 and Prompt 2.

### Prompt 1
Can you explain what SVG is? How is it programmed?

### Response 1
SVG stands for Scalable Vector Graphics. It's an XML-based format for creating two-
dimensional graphics that can scale to any size without losing quality—unlike raster images 
(like JPEGs or PNGs) which are made of pixels and get blurry when enlarged.

**How SVG works**
SVG describes images using mathematical shapes and paths rather than pixels. When you 
zoom in on an SVG, your browser recalculates the math to redraw it perfectly at the new size.

**How it's programmed**
SVG is written as text, similar to HTML. Here's a simple example:

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
    <circle cx="100" cy="100" r="50" fill="blue" />
    <rect x="25" y="25" width="50" height="50" fill="red" />
</svg>

This creates a blue circle and a red rectangle. The syntax uses:
    - Basic shapes: <circle>, <rect>, <ellipse>, <line>, <polygon>
    - Paths: <path> for complex custom shapes using commands like M (move), L (line), C
    (curve)
    - Attributes: Position (x,y), size (width, height, radius), appearance (fill, stroke, opacity)

You can also add gradients, filters, animations, and text. SVG can be embedded directly in
HTML, saved as .svg files, or manipulated with CSS and JavaScript just like HTML elements.

Because it's vector-based and text-based, SVG is perfect for logos, icons, diagrams, and any
graphics that need to look sharp at any size.

### Changes 1
This project only deals with SVG primitives, so I ignored <ellipse>, <polygon>, <path>, and
features like gradients, filters, etc.

### Prompt 2
I'm getting an error from my Makefile:
Makefile:82: *** recipe commences before first target. Stop.

### Response 2
This Makefile error means line 82 has a recipe command (an indented line starting with a
tab) but there's not target defined above it.

**Quick diagnostic steps:**
Check line 82 and the lines above it. Look for:

1. **Is line 82 indented with a tab?** If so, it's being interpreted as a recipe command, but there's no target for it to belong to.
2. **Is there a target with a colon above it?** You need something like:

target_name:
    command here

3. **Did a previous target definition get broken?** Common issues:
    - Missing colon after the target name
    - A comment accidentally splitting a target from its recipe
    - A variable assignment where a target should be
4. **Tabs vs spaces issue?** Recipe lines MUST use a literal tab character, not spaces. If you
have spaces, Make won't recognize it as a recipe, which can cascade into confusion.

**To fix it:**
Look at lines 80-83 in your Makefile. You should see a pattern like:

some_target: dependencies
    command to run

If line 82 is indented but there's no target: line immediately before it (or the target line is
malformed), that's your problem.

Can you check what's on lines 80-82 of your Makefile? That would help pinpoint the exact
issue.

### Changes 2
Upon highlighting my code, VS Code showed that I had a space-tab on Line 81 that made it
look aligned with Line 82, which *did* have a sole tab character. Therefore, I only ended
up using #4 on the list of what Claude suggested that I look for.