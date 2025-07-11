# WikiLoop Galaxy

An interactive network visualization tool that maps Wikipedia articles and their interconnections using the Wikipedia API. Built with D3.js for dynamic graph rendering and real-time exploration.

**🌐 Web App**: https://galaxy.wikiloop.org  
**📁 Source Code**: https://github.com/wikiloop/galaxy  
**📖 Wikipedia Page**: [[WP:WikiLoop Galaxy]]

## Features

### Core Functionality
- **Bidirectional Link Traversal**: Explores both outbound links (FROM articles) and inbound links (TO articles)
- **Real-time Graph Building**: Starts with a root article and progressively builds the network
- **Interactive Expansion**: Click any node to expand it with 10 more connected articles
- **Link Validation**: Checks page existence to handle broken Wikipedia links

### Visual Design
- **Obsidian-style Dark Theme**: Clean, modern interface optimized for graph exploration
- **Color-coded Nodes**:
  - 🟢 **Green**: Root article (starting point)
  - 🔵 **Blue/Teal**: Valid Wikipedia articles (1st/2nd degree)
  - 🔴 **Red**: Missing/non-existent pages (red links)
  - 🟡 **Yellow Border**: Expandable nodes with pulsing animation
- **Force-directed Layout**: Natural node positioning with physics simulation
- **Zoom & Pan**: Navigate large graphs with mouse controls

### Interaction
- **Click**: Expand node to reveal 10 more inbound + 10 outbound links
- **Ctrl/Cmd + Click**: Open Wikipedia article in new tab
- **Drag**: Move nodes around the canvas
- **Scroll**: Zoom in/out of the graph

## Technical Architecture

### API Integration
- Uses Wikipedia REST API for article links and backlinks
- Implements proper error handling and rate limiting
- Filters out non-article links (categories, templates, files)
- Validates page existence before adding to graph

### Graph Management
- **Node Deduplication**: Prevents duplicate articles in the network
- **Link Direction**: Maintains proper directional relationships
- **Expansion Tracking**: Prevents re-expansion of already processed nodes
- **Memory Efficient**: Limits link counts to prevent browser overload

### Performance
- **Lazy Loading**: Only fetches data when needed
- **Batch Processing**: Processes multiple links efficiently
- **Visual Feedback**: Shows loading states and progress indicators
- **Responsive Design**: Adapts to different screen sizes

## Usage

1. **Start**: Open `index.html` in a web browser
2. **Explore**: The graph begins with "Artificial Intelligence" as the root
3. **Expand**: Click any node to reveal more connected articles
4. **Navigate**: Use mouse to zoom, pan, and drag nodes
5. **Visit**: Ctrl/Cmd+Click to open Wikipedia pages

## Configuration

### Default Settings
- **Root Article**: "Artificial_intelligence"
- **Link Limit**: 10 outbound + 10 inbound per expansion
- **Traversal Depth**: 2 degrees from root (configurable)
- **Node Limit**: Unlimited (browser memory dependent)

### Customization
To change the root article, modify line 188 in `index.html`:
```javascript
this.startArticle = "Your_Article_Title";
```

## Console Logging

The application provides detailed console output:
- 🚀 Initialization status
- 📖 Articles being processed
- 🔍 Links discovered and extracted
- ➕ Nodes being added to graph
- 🔗 Links being created
- ⚠️ Missing pages and errors
- 🖱️ User interactions

## Browser Compatibility

- **Modern Browsers**: Chrome, Firefox, Safari, Edge
- **Requirements**: ES6+ support, SVG rendering
- **Dependencies**: D3.js v7 (loaded via CDN)

## File Structure

```
├── index.html          # Complete single-file application
├── README.md           # This documentation
└── wiki-graph.html     # (Previous version)
```

## Technical Details

### API Endpoints Used
- **Outbound Links**: `https://en.wikipedia.org/w/api.php?action=query&prop=links`
- **Inbound Links**: `https://en.wikipedia.org/w/api.php?action=query&list=backlinks`
- **Page Validation**: `https://en.wikipedia.org/w/api.php?action=query&titles=`

### Data Flow
1. Initialize with root article
2. Fetch outbound + inbound links
3. Validate page existence
4. Add valid pages as nodes
5. Create directional links
6. Update visual representation
7. Enable click-to-expand for all nodes

## Roadmap

### 1. Wikipedia User Script
Create a Wikipedia user script that hardcore Wikipedians can install directly on Wikipedia pages to instantly visualize article networks without leaving the site.

**Features:**
- One-click graph generation from any Wikipedia article
- Seamless integration with Wikipedia's interface
- Customizable settings for power users
- Export capabilities for research and analysis

### 2. Browser Extensions
Develop browser extensions for easy installation by non-technical users across all major browsers:

- **Chrome Extension**: Available on Chrome Web Store
- **Firefox Extension**: Available on Mozilla Add-ons
- **Edge Extension**: Available on Microsoft Edge Add-ons
- **Safari Extension**: Available on Mac App Store
- **DuckDuckGo Extension**: Privacy-focused browsing integration

**Benefits:**
- No technical setup required
- Automatic updates
- One-click installation
- Cross-browser compatibility

### 3. Performance Optimization with Caching
Implement intelligent caching system to dramatically improve performance and reduce Wikipedia API load.

**Caching Strategy:**
- Local storage for frequently accessed articles
- Session-based cache for current browsing session
- Intelligent cache invalidation and updates
- Offline capability for previously loaded graphs

**Performance Improvements:**
- Faster graph loading times
- Reduced API calls to Wikipedia
- Better user experience with instant results
- Bandwidth optimization for mobile users

## Future Enhancements

- **Search Functionality**: Custom root article selection ✅ (Completed)
- **Export Options**: Save graph as image or data
- **Filtering**: Hide/show specific link types
- **Clustering**: Group related articles
- **Performance**: Virtual rendering for large graphs
- **Mobile**: Touch-optimized interactions

## License

MIT License - Feel free to use and modify for your projects.