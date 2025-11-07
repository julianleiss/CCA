# Actor-Network Graph Visualization

A D3.js-based interactive visualization for rendering actor-network graphs with force-directed layout.

## Features

### Nodes
- **Visual representation**: Circular nodes
- **Size scaling**: Radius scales linearly by `influence` value (8px to 38px)
- **Color coding** by group:
  - **humano**: #2E7D32 (Green)
  - **artefacto**: #1565C0 (Blue)
  - **no_humano**: #EF6C00 (Orange)
  - **institucion**: #6A1B9A (Purple)
  - **intervencion**: #00796B (Teal)
- **Labels**: Always visible for top 8 most influential nodes with collision-aware positioning
- **Tooltips**: Full label, group, influence, and level displayed on hover (throttled for performance)
- **Collision avoidance**: Prevents node overlap
- **Keyboard accessible**: Fully keyboard-focusable with ARIA labels

### Edges (Links)
- **Directed arrows**: Visual indication of relationship direction
- **Stroke width**: Based on `w` value (1-5)
- **Dashed lines**: Applied when `pol` is "-"
- **Tooltips**: Shows relationship type (`rel`) and confidence (`conf`)
- **Accessibility**: Title elements for screen readers

### Layout
- **Force-directed**: Automatic positioning with physics simulation
- **Level-based clustering**: Soft clustering by `level` (micro/meso/macro)
- **Interactive**: Drag nodes to reposition, with auto-return on release
- **Responsive**: Adapts to window resize
- **Optimized rendering**: Uses requestAnimationFrame for smooth animations

### Interactive Controls

#### Filtering
- **Group Filters**: Toggle visibility of nodes by group (humano, artefacto, no_humano, institucion, intervencion)
- **Intervention-Only Mode**: Quick toggle to show only intervention nodes and their connections
- **Dynamic Updates**: Links automatically hide when connected nodes are filtered out

#### Search & Highlight
- **Search Bar**: Find nodes by label (partial match, case-insensitive)
- **Visual Feedback**: Matching nodes highlighted in pink, non-matching faded to 15% opacity
- **Link Highlighting**: Connected links also highlighted
- **Keyboard Shortcut**: Press Escape to clear search

#### Navigation
- **Zoom & Pan**: Mouse wheel/trackpad zoom, click-and-drag to pan
- **Touch Support**: Full touch gesture support for mobile devices
- **Zoom Controls**: +/- buttons for precise zoom, reset button to restore default view
- **Smooth Transitions**: Animated zoom with 300-500ms duration

#### Export
- **SVG Export**: Download vector graphics for editing in Illustrator, Inkscape, etc.
- **PNG Export**: High-resolution (2x) raster export for presentations and documents
- **Preserves State**: Exports current zoom level and visibility state

### Accessibility Features

- **WCAG Compliant**: Meets accessibility standards for interactive visualizations
- **Keyboard Navigation**:
  - Tab through nodes and controls
  - Enter/Space to highlight selected node
  - Escape to clear search
- **ARIA Labels**: Comprehensive labels for screen readers
  - Nodes: "Label, group name group, influence N"
  - Controls: Descriptive labels for all buttons and inputs
  - Regions: Proper role attributes (toolbar, img, tooltip)
- **Focus Indicators**: Clear visual focus states with dashed borders
- **Title Elements**: SVG title tags for native browser tooltips
- **Color Contrast**: All colors meet WCAG AA standards
- **Readable Text**: Bold text with white shadow for maximum legibility

## Usage

### Quick Start

Simply open `actor-network-visualization.html` in a modern web browser.

### Adding Your Data

Replace the sample data in the `<script>` section with your actual dataset. The data structure must match:

```javascript
const data = {
    nodes: [
        {
            id: "unique_id",           // Required: Unique identifier
            label: "Full Node Name",   // Required: Full display name
            short_label: "Short",      // Required: Abbreviated name for permanent labels
            influence: 75,             // Required: Numeric value (affects node size)
            group: "humano",           // Required: One of: humano, artefacto, no_humano, institucion, intervencion
            level: "meso"              // Required: One of: micro, meso, macro
        },
        // ... more nodes
    ],
    links: [
        {
            source: "node_id_1",       // Required: Source node ID
            target: "node_id_2",       // Required: Target node ID
            rel: "relationship name",  // Required: Relationship description
            w: 3,                      // Required: Weight/width (1-5)
            pol: "+",                  // Required: Polarity ("+" or "-")
            conf: 0.85                 // Required: Confidence (0-1)
        },
        // ... more links
    ]
};
```

### Data Requirements

**Node Fields** (all required):
- `id`: Unique identifier (string)
- `label`: Full name for tooltips (string)
- `short_label`: Abbreviated name for permanent labels (string)
- `influence`: Numeric value for size scaling (number)
- `group`: Category (must be one of: humano, artefacto, no_humano, institucion, intervencion)
- `level`: Clustering level (must be one of: micro, meso, macro)

**Link Fields** (all required):
- `source`: ID of source node (string)
- `target`: ID of target node (string)
- `rel`: Relationship description (string)
- `w`: Edge weight for width (number, 1-5)
- `pol`: Polarity (string, "+" or "-")
- `conf`: Confidence level (number, 0-1)

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| Tab | Navigate between nodes and controls |
| Enter / Space | Highlight selected node in search |
| Escape | Clear search and reset highlighting |
| Mouse Wheel | Zoom in/out |
| Click + Drag | Pan the graph |

## Technical Details

- **Library**: D3.js v7
- **Layout Algorithm**: Force-directed with collision detection
- **Performance Optimizations**:
  - requestAnimationFrame for smooth rendering
  - Throttled hover events (50ms) to reduce overhead
  - Collision-aware label positioning
  - Debounced resize handler (250ms)
- **Interactivity**: Drag-and-drop nodes, hover tooltips, zoom/pan, keyboard navigation
- **Responsive**: Automatically adjusts to window size
- **Touch Support**: Full gesture support for mobile and tablet devices
- **No external dependencies** except D3.js (loaded via CDN)

## Browser Compatibility

Works in all modern browsers supporting ES6+ and SVG:
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)

## Customization

Key parameters that can be adjusted in the code:

- **Node size range**: Modify `radiusScale.range([8, 38])`
- **Link width range**: Modify `widthScale.range([1, 5])`
- **Force strengths**: Adjust values in simulation forces
- **Colors**: Modify the `colors` object
- **Top N labels**: Change `slice(0, 8)` to show more/fewer permanent labels

## License

MIT
