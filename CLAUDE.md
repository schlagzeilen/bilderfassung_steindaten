# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the "bilderfassung_steindaten" (Stone Data Image Capture) project - a web application for capturing and processing concrete block test data using OCR technology.

## Current State

This is a single-page web application built with vanilla HTML, CSS, and JavaScript featuring:
- Camera integration for capturing concrete block images
- OCR (Optical Character Recognition) using Tesseract.js for automatic data extraction
- Button-based UI for batch, board, and position selection
- CSV export functionality for test results
- Configurable parameters and OCR toggle

## Architecture

### Technology Stack
- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES6+)
- **OCR Library**: Tesseract.js v4.1.1 (loaded via CDN)
- **Camera API**: MediaDevices.getUserMedia() for camera access
- **Data Storage**: Browser localStorage (implicit via JavaScript variables)
- **Export Format**: CSV file generation client-side

### Key Features
1. **Camera Integration**: Auto-starts camera on page load, continuous workflow
2. **OCR Processing**: Automatic detection of batch numbers, board numbers, and position letters
3. **Button Grids**: 6-buttons-per-row layout for batch (1-12), board (1-12), and position (A-L) selection
4. **Configurable Parameters**: All button sets can be customized via configuration area
5. **OCR Toggle**: Checkbox to enable/disable OCR (hides camera when off)
6. **One-liner Results**: Compact display format (B: 1, Bd: 2, P: A, T: PASS)
7. **Continuous Workflow**: After adding entry, automatically prepares for next photo

### File Structure
```
/
├── index.html          # Complete single-page application
├── CLAUDE.md          # This documentation file
└── README.md          # Project readme (empty)
```

## Workflow

### Standard Usage Flow
1. **Page Load**: Camera permission requested once, camera starts automatically
2. **Select Numbers**: Choose batch and board numbers (stay selected across photos)
3. **Capture Photo**: Take picture of concrete block
4. **OCR Processing**: Automatic detection fills form fields (if OCR enabled)
5. **Verify/Adjust**: Check OCR results, select position letter, choose PASS/FAIL
6. **Add Entry**: Click "Add Entry" - clears selections and prepares for next photo
7. **Export**: Use "Export CSV" button to download results

### Configuration Options
- **Letters**: Customize available position letters (default A-L)
- **Batch Numbers**: Customize available batch numbers (default 1-12, comma-separated)
- **Board Numbers**: Customize available board numbers (default 1-12, comma-separated)
- **OCR Toggle**: Enable/disable automatic text detection (hides camera when off)

## UI Layout

### Main Interface (Top to Bottom)
1. **Camera Section**: Live video feed, Capture/Retake buttons
2. **Form Section**: Batch/Board/Position button grids, PASS/FAIL buttons, Add Entry button
3. **Results List**: Compact one-line entries with delete buttons
4. **Export Section**: Full-width CSV export button
5. **Configuration**: OCR toggle, button customization (bottom of page)

### Button Styling
- **Selection Buttons**: 6-per-row grid, blue highlight when selected
- **Action Buttons**: Full-width, large (Add Entry, Export CSV)
- **Config Buttons**: Full-width, medium size
- **Delete Buttons**: Fixed width, consistent alignment

## Technical Implementation Notes

### Camera Management
- Single permission request on page load
- Stream stays alive between photos (no re-permission needed)
- Auto-restart after each entry addition
- Proper cleanup on page unload

### OCR Processing
- Processes three regions: batch (top-left), board (bottom-left), position (right)
- Uses parallel processing for efficiency
- Only runs when OCR checkbox is enabled
- Graceful fallback to manual entry if OCR fails

### Data Management
- In-memory array storage for entries
- Each entry: {id, batch, board, position, testResult, timestamp}
- Automatic CSV generation with proper escaping
- Delete functionality with immediate UI update

## Development Notes

- **No Build Process**: Direct HTML file, no compilation needed
- **No Dependencies**: Tesseract.js loaded via CDN
- **Mobile-Friendly**: Responsive design, touch-optimized buttons
- **Camera-First**: Designed for mobile devices with rear cameras
- **Performance**: Minimal DOM manipulation, efficient event handling

## Browser Requirements

- **Modern Browser**: ES6+ support required
- **Camera Access**: MediaDevices.getUserMedia() support
- **Canvas API**: For image processing
- **File API**: For CSV download
- **Tested**: Chrome/Safari on mobile devices

## Future Enhancement Areas

- **Offline Capability**: Service worker for offline usage
- **Data Persistence**: LocalStorage or IndexedDB for data backup
- **Batch Processing**: Multi-block processing optimizations
- **Image Storage**: Optional image archiving with entries
- **Export Formats**: Additional export options (Excel, JSON)