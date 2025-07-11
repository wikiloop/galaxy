# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file Wikipedia graph visualization application built with D3.js. The application creates an interactive network graph that maps Wikipedia articles and their interconnections using the Wikipedia API.

## Architecture

### Core Components

**WikipediaGraph Class** (`index.html` lines 182+)
- Main application class that manages the entire graph lifecycle
- Handles D3.js simulation, Wikipedia API calls, and user interactions
- Key data structures:
  - `nodes`: Map of article titles to node objects
  - `links`: Set of directional connections between articles
  - `processedArticles`: Set tracking already-fetched articles
  - `expandedNodes`: Set tracking manually expanded nodes
  - `queue`: Array for breadth-first article processing

**API Integration**
- `fetchArticleLinks()`: Retrieves both outbound and inbound links from Wikipedia API
- `checkPageExists()`: Validates Wikipedia page existence before adding nodes
- Uses Wikipedia's MediaWiki API with CORS-enabled requests

**Graph Management**
- Bidirectional link traversal (outbound: FROM article, inbound: TO article)
- Node deduplication prevents duplicate articles
- Link direction maintained for proper graph structure
- Expansion tracking prevents re-processing of nodes

## Key Configuration

### Default Settings
- **Root Article**: `"Artificial_intelligence"` (line 224 in index.html)
- **Link Limits**: 10 outbound + 10 inbound per expansion
- **Node Colors**: Green (root), Blue/Teal (valid), Red (missing), Yellow border (expandable)

### Customization Points
- Change root article by modifying `this.startArticle` on line 224
- Adjust link limits in `fetchArticleLinks()` method (`pllimit` and `bllimit` parameters)
- Modify node colors in CSS section (lines 36-67)
- Adjust D3.js force simulation parameters (lines 213-217)

## Development Commands

Since this is a single-file HTML application, development is straightforward:

**Run Application**
```bash
# Open in browser (any modern browser)
open index.html
# Or serve via local server
python -m http.server 8000
```

**Debug and Development**
- Open browser developer tools to view console logs
- The application provides extensive console logging with emojis for easy debugging
- Use browser's network tab to monitor Wikipedia API calls

## API Endpoints Used

- **Outbound Links**: `https://en.wikipedia.org/w/api.php?action=query&prop=links`
- **Inbound Links**: `https://en.wikipedia.org/w/api.php?action=query&list=backlinks`
- **Page Validation**: `https://en.wikipedia.org/w/api.php?action=query&titles=`

## User Interaction Model

- **Click**: Expand node with 10 more inbound + outbound links
- **Ctrl/Cmd + Click**: Open Wikipedia article in new tab
- **Drag**: Move nodes around canvas
- **Scroll**: Zoom in/out of graph
- **Reset/Pause**: Control graph building process

## Technical Constraints

- Wikipedia API rate limiting: Built-in delays between requests
- Browser memory: No hard node limits, but performance degrades with very large graphs
- CORS: Uses `origin=*` parameter for Wikipedia API access
- ES6+ required: Uses modern JavaScript features (classes, async/await, arrow functions)

## Data Flow

1. Initialize with root article
2. Fetch outbound + inbound links via Wikipedia API
3. Validate page existence for each link
4. Add valid pages as nodes, missing pages as red nodes
5. Create directional links maintaining proper graph structure
6. Update D3.js visualization with new nodes/links
7. Enable click-to-expand for all nodes

## File Structure

- `index.html`: Complete single-file application (HTML, CSS, JavaScript)
- `README.md`: User documentation and feature description
- `CLAUDE.md`: This development guide