# Illuminare - Medieval Missal Editor

**Illuminare** is a sophisticated web-based editor for creating authentic medieval missal reproductions with full liturgical accuracy, decorative elements, and professional PDF output. Built for scholars, liturgists, and artists who need to create 1:1 facsimiles of historical manuscripts.

## Overview

Illuminare bridges the gap between historical manuscript traditions and modern digital publishing. It provides a complete toolkit for creating medieval missals with:

- **Object-based page composition** with drag-and-drop interface
- **Liturgical text catalogs** with searchable prayers and readings  
- **Gregorian chant integration** via Gregobase API
- **Medieval decorative elements** including illuminated initials and borders
- **Professional PDF output** via printpdf.js integration
- **Manuscript-accurate typography** with historical font support

## ✨ Key Features

### 🎨 Professional Editor Interface
- **Microsoft Office-style ribbon interface** with collapsible panels
- **Object-oriented design system** - every element is a configurable object
- **Real-time visual feedback** with drag-and-drop positioning
- **Dynamic properties panel** that adapts to selected object type
- **Multi-page project management** with page thumbnails and navigation

### 📿 Liturgical Content Management
- **Prayer catalog** with Latin ordinary and proper texts
- **Gregorian chant integration** with Gregobase search (API ready)
- **Rubric support** with traditional red text formatting
- **Initial capital system** with text flow integration
- **Connected objects** - prayers can automatically include initial capitals

### 🖼️ Medieval Manuscript Features
- **Illuminated initial capitals** with SVG conversion capabilities
- **Decorative border systems** (floral, geometric, Celtic)
- **Medieval color palette** with authentic reds, golds, and blacks
- **Historical typography** supporting Gothic, Uncial, and Carolingian scripts
- **Ornamental elements** library with traditional symbols

### 📄 Professional Output
- **printpdf.js integration** for high-quality PDF generation
- **Coordinate system conversion** from editor to PDF layout
- **Resource management** with automatic image and font embedding
- **Index generation** with automatic section tracking
- **Print-ready output** with proper margins and page layout

## 🏗️ Architecture

### Object System
Every page element is a `PageObject` instance with:

```javascript
class PageObject {
  id: string           // Unique instantiation identifier
  type: string         // Object type (text, prayer, initial, etc.)
  content: object      // Semantic content (what it represents)
  position: {x, y}     // Page coordinates
  dimensions: {w, h}   // Object size
  style: object        // Display properties
  connected: array     // Links to related objects
}
```

### Supported Object Types
- **Text Block** - Free-form text with font control
- **Prayer** - Liturgical prayers with title/text structure
- **Initial Capital** - Drop caps with SVG conversion
- **Image** - Uploaded graphics with positioning
- **Chant** - Gregorian notation (SVG from Gregobase)
- **Decoration** - Ornamental elements and borders

### Project Structure
```javascript
{
  name: "Project Name",
  pages: [
    { objects: [PageObject, ...] }
  ],
  resources: {
    images: { id: {name, data, type} },
    fonts: { id: {name, data, type} }
  },
  settings: { pageSize, margins, etc. }
}
```

## 🚀 Getting Started

### Prerequisites
- Modern web browser with ES6 support
- printpdf.js WASM module (for PDF export)
- Web server (for file operations)

### Installation
1. Clone the repository:
```bash
git clone https://github.com/yourusername/illuminare.git
cd illuminare
```

2. Set up printpdf.js:
```bash
# Copy printpdf WASM files to pkg/ directory
cp path/to/printpdf.js pkg/
cp path/to/printpdf_bg.wasm pkg/
```

3. Serve the application:
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .

# Using PHP
php -S localhost:8000
```

4. Open `http://localhost:8000` in your browser

### Quick Start
1. **Create a new project** from the Home ribbon
2. **Select an object tool** from the sidebar (Text, Prayer, etc.)
3. **Click on the page** to place the object
4. **Configure properties** in the right panel
5. **Drag objects** to reposition them
6. **Export to PDF** when ready

## 📖 Usage Guide

### Creating Pages
- Use **Add Page** from the ribbon or sidebar
- Navigate between pages with the page navigator
- Each page maintains its own object collection

### Working with Objects
1. **Placement**: Select tool from sidebar, click on canvas
2. **Selection**: Click any object to select and configure
3. **Movement**: Drag objects around the page
4. **Resizing**: Use resize handles on selected objects
5. **Properties**: Configure in the right panel
6. **Deletion**: Select object and press Delete key

### Prayer Workflow
1. Browse the **Prayers catalog** in the sidebar
2. **Double-click** a prayer to add it to the page
3. **Configure** title, text, and formatting options
4. **Enable initial capital** in properties if desired
5. **Position** the prayer block appropriately

### Initial Capitals
1. Add an **Initial** object to the page
2. Set the **letter** in properties
3. Choose **style**: Simple, Decorated, or Illuminated
4. **Convert to SVG** for custom artwork
5. **Position** at the start of text blocks

### Chant Integration
1. Select **Chant** tool and place on page
2. Use **Search Gregobase** in properties panel
3. **Import SVG notation** from search results
4. **Adjust size** and positioning as needed

### Resource Management
1. **Upload images** via Resources panel
2. **Upload fonts** for custom typography
3. **Select resources** in object properties
4. Resources are **automatically embedded** in PDF

### PDF Export
1. Use **Export PDF** from the Home ribbon
2. The system **converts all objects** to printpdf operations
3. **Resources are included** automatically
4. **Download** the generated PDF file

## Technical Details

### Coordinate System
- **Editor**: Pixels with (0,0) at top-left
- **PDF**: Millimeters with (0,0) at bottom-left
- **Conversion**: Automatic during PDF generation

### Object Serialization
Objects are serialized to JSON for project save/load:
```javascript
{
  id: "obj_123_abc",
  type: "prayer", 
  x: 100, y: 150,
  width: 200, height: 100,
  content: {
    title: "Kyrie Eleison",
    text: "Kyrie eleison...",
    hasInitial: true
  }
}
```

### PDF Generation
Each object type implements `toPrintPdfOps()`:
```javascript
toPrintPdfOps() {
  return [
    { type: "set-text-cursor", data: { pos: {x: mmX, y: mmY} } },
    { type: "write-text-builtin-font", data: { items: [text], size: 12, font: "times-roman" } }
  ];
}
```

### printpdf.js Integration
The editor generates complete printpdf document structures:
- **Metadata** with document information
- **Resources** with embedded images and fonts  
- **Pages** with operation sequences
- **Coordinate conversion** for proper layout

## 🔮 Roadmap

### Phase 1: Core Features ✅
- [x] Object-based editor
- [x] Basic liturgical catalog
- [x] PDF generation framework
- [x] Resource management

### Phase 2: Enhanced Functionality
- [ ] Gregobase API integration
- [ ] Advanced initial capital SVG generation
- [ ] Text flow algorithms for initials
- [ ] Border and decoration templates
- [ ] Font subsetting for PDF optimization

### Phase 3: Professional Features
- [ ] Index and table of contents generation
- [ ] Liturgical calendar integration
- [ ] Manuscript template library
- [ ] Advanced typography controls
- [ ] Collaborative editing features

### Phase 4: Scholarly Tools
- [ ] Critical apparatus support
- [ ] Manuscript comparison tools
- [ ] Historical accuracy validation
- [ ] Export to multiple formats (LaTeX, InDesign)

## Contributing

We welcome contributions from liturgists, developers, and manuscript scholars!

### Development Setup
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes with tests
4. Commit: `git commit -m 'Add amazing feature'`
5. Push: `git push origin feature/amazing-feature`
6. Open a Pull Request

### Contribution Areas
- **Liturgical Content**: Expanding prayer and chant catalogs
- **Typography**: Adding historical font support
- **Decorations**: Creating SVG ornament libraries
- **API Integration**: Connecting external liturgical databases
- **Documentation**: Improving user guides and examples

### Code Style
- ES6+ JavaScript with clear object-oriented design
- Meaningful variable names and comprehensive comments
- Modular architecture with separation of concerns
- Responsive CSS with mobile considerations

## Resources

### Liturgical References
- [Gregobase](http://gregobase.selapa.net/) - Gregorian chant database
- [Corpus Christi Watershed](https://www.ccwatershed.org/) - Sacred music resources
- [CPDL](http://www.cpdl.org/) - Choral Public Domain Library

### Technical Documentation
- [printpdf.js Documentation](https://docs.rs/printpdf/) - PDF generation library
- [Medieval Unicode](http://www.mufi.info/) - Character encoding standards
- [Digital Scriptorium](https://digital.library.berkeley.edu/scriptorium/) - Manuscript examples

### Manuscript Studies
- [British Library Digitised Manuscripts](https://www.bl.uk/manuscripts/)
- [Vatican Apostolic Library](https://digi.vatlib.it/)
- [Bibliotheque Nationale de France](https://gallica.bnf.fr/)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **printpdf.js team** for the excellent PDF generation library
- **Gregobase contributors** for maintaining the chant database
- **Medieval manuscript scholars** who preserve these traditions
- **Open source community** for tools and inspiration

## Contact

- **Project Lead**: [Your Name](mailto:your.email@example.com)
- **Documentation**: [docs@illuminare.org](mailto:docs@illuminare.org)  
- **Issues**: [GitHub Issues](https://github.com/yourusername/illuminare/issues)
- **Discussions**: [GitHub Discussions](https://github.com/fschutt/illuminare/discussions)
