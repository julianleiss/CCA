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
- **Labels**: Always visible for top 8 most influential nodes (short labels)
- **Tooltips**: Full label, group, influence, and level displayed on hover
- **Collision avoidance**: Prevents node overlap

### Edges (Links)
- **Directed arrows**: Visual indication of relationship direction
- **Stroke width**: Based on `w` value (1-5)
- **Dashed lines**: Applied when `pol` is "-"
- **Tooltips**: Shows relationship type (`rel`) and confidence (`conf`)

### Layout
- **Force-directed**: Automatic positioning with physics simulation
- **Level-based clustering**: Soft clustering by `level` (micro/meso/macro)
- **Interactive**: Drag nodes to reposition, with auto-return on release
- **Responsive**: Adapts to window resize

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

## Technical Details

- **Library**: D3.js v7
- **Layout Algorithm**: Force-directed with collision detection
- **Interactivity**: Drag-and-drop nodes, hover tooltips
- **Responsive**: Automatically adjusts to window size
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
