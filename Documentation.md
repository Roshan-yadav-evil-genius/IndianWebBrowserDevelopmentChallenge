# Architecture Development Analysis report

## Rendering Engine

### Parsing

- **Construction of DOM**: Parsing of Html text string into DOM

- **Sub resource Loading**: Concurrently pre loads tags like img or link

- **JavaScript can block Parsing**: as it can the shape of DOM (this script is executed by JS engine), tags like async and defer can change this behaviour

- **Style Calculation**: The main thread parses CSS and determines the computed style for each DOM node. (Some predefined computed styles are already present e.g., h1 text is bigger than of h2) (can happen both concurrently and after DOM creation)

- **Layout**: Now main thread goes through DOM and computed styles and creates a layout tree. (IT have information like x y coordinates and bounding box sizes)

- **Paint**: the main thread walks the layout tree to create paint records. Paint record is a note of painting process like "background first, then text, then rectangle".

### Compositing

- **Dividing into layers**: In order to find out which elements need to be in which layers, the main thread walks through the layout tree to create the layer tree.

- **Raster and composite off of the main thread**: Rasterization of layer in small tiles (draw quads)

- **Compositor frame**: A compositor frame is made from these tiles

- Sharing of frame to browser processes
