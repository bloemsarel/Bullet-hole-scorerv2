# 🎯 25 Target Scorer

A fully offline-capable Progressive Web App (PWA) for automatically detecting and scoring bullet holes on 25-target shooting sheets.

## Features

- **📸 Instant Capture**: Take photos directly from your device camera or select existing images
- **🤖 Automatic Detection**: AI-powered bullet hole detection and scoring
- **💯 Precise Scoring**: 10-ring scoring system with X-ring detection
- **💾 Local Storage**: Save results with shooter identification for later review
- **📊 History Management**: View, filter, and delete saved scoring sessions
- **🔌 Fully Offline**: Works completely offline - no internet required at the range
- **⚙️ Adjustable Settings**: Fine-tune detection parameters for different lighting and target conditions
- **📱 Mobile-Optimized**: Designed for smartphones and tablets

## Quick Start

### ⚠️ Important: Service Worker Requirements
Service Workers (for offline functionality) **only work on**:
- ✅ **HTTPS** websites (like GitHub Pages)
- ✅ **localhost** (http://localhost:8000)
- ❌ **NOT** when opening HTML file directly (file:// protocol)

**Good news:** The app works perfectly even without Service Worker - you just won't have offline caching. All features (detection, scoring, saving) still work!

### Online Access (Recommended)
1. Visit the hosted version at: `https://bloemsarel.github.io/Bullet-hole-scorer/`
2. Tap "Add to Home Screen" when prompted (for offline use)

### Local Testing
To test locally, you must use a web server:
```bash
# Python 3
python -m http.server 8000

# Python 2  
python -m SimpleHTTPServer 8000

# Node.js
npx http-server
```
Then open: `http://localhost:8000`

### Local Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/bloemsarel/Bullet-hole-scorer.git
   ```
2. Open `index.html` in a web browser
3. For offline use, host the files on any web server (even locally with Python's SimpleHTTPServer)

### Android Installation (Offline Use)
1. Open the app in Chrome or Firefox on your Android device
2. Tap the menu (⋮) and select "Add to Home Screen" or "Install App"
3. The app will install as a standalone application
4. Works completely offline once installed!

## Usage Instructions

### 1. Scoring a Target

1. **Enter Shooter ID**: Type an alphanumeric identifier (e.g., "ALPHA01", "SHOOTER-123")
2. **Capture Target**: 
   - Tap "📸 CAPTURE TARGET" to take a photo with your camera
   - Or tap "📁 SELECT IMAGE" to choose from gallery
3. **Automatic Processing**: The app automatically:
   - Detects the 5x5 target grid
   - Identifies bullet holes in each target
   - Calculates scores based on distance from center
   - Displays total score and statistics
4. **Review Results**: Check the marked-up image showing all detected holes
5. **Save**: Tap "💾 SAVE RESULTS" to store the session

### 2. Viewing History

1. Tap the "📊 HISTORY" button at the top
2. Browse all saved scoring sessions
3. Tap "👁️ VIEW" on any record to see full details
4. Tap "🗑️ DELETE" to remove a specific record
5. Use "🗑️ CLEAR ALL" to delete all saved data

### 3. Adjusting Detection Settings

If the app isn't detecting holes correctly, adjust these settings:

- **Hole Darkness**: How dark a spot must be to count as a hole (lower = more sensitive)
- **Min Hole Size**: Minimum size in pixels (increase if detecting noise as holes)
- **Max Hole Size**: Maximum size in pixels (decrease if combining multiple holes)

**Tip**: Take a test photo and adjust settings until detection is accurate, then use those settings for all subsequent shots.

## Scoring System

The app uses a standard 10-ring bullseye scoring system:

- **10 points + X**: Dead center (X-ring)
- **10 points**: Inner ring
- **9-1 points**: Decreasing scores based on distance from center
- **0 points**: No hit detected

**Statistics Displayed**:
- Total Score (sum of all 25 targets)
- Shots Fired (total bullet holes detected)
- X-Ring Hits (perfect center shots)
- Average Score per Shot
- Targets Hit (how many of 25 targets have at least one hole)

## Technical Details

### Technologies Used
- **HTML5 Canvas**: Image processing and hole detection
- **LocalStorage API**: Offline data persistence
- **Service Workers**: PWA offline functionality
- **Web Manifest**: App installation support
- **Custom Fonts**: Orbitron & Rajdhani for tactical aesthetics

### How Detection Works

1. **Grid Detection**: Finds the bounding box of the target sheet
2. **Cell Division**: Divides into 5×5 grid (25 individual targets)
3. **Hole Detection**: Uses flood-fill algorithm to find dark spots (holes)
4. **Scoring**: Calculates distance from hole center to target center
5. **Visualization**: Draws detection results on canvas

### Browser Compatibility
- ✅ Chrome/Edge (Android & Desktop)
- ✅ Firefox (Android & Desktop)
- ✅ Safari (iOS & macOS)
- ✅ Samsung Internet

## Tips for Best Results

### Photography
- **Good Lighting**: Ensure even lighting on the target sheet
- **Minimal Shadows**: Avoid casting shadows on the sheet
- **Straight Angle**: Hold phone parallel to target (not at an angle)
- **Full Frame**: Capture the entire sheet with some margin
- **Focus**: Make sure the image is sharp and in focus

### Target Sheets
- **High Contrast**: Black targets on white paper work best
- **Clean Background**: Minimal markings outside targets
- **Standard Layout**: Works best with evenly-spaced 5×5 grids

### Common Issues

**Problem**: Console says "Service Worker registration failed"
- **Cause**: Service Workers require HTTPS or localhost (won't work with file:// protocol)
- **Solution 1**: Deploy to GitHub Pages (uses HTTPS automatically)
- **Solution 2**: Run a local web server (see Quick Start above)
- **Solution 3**: Ignore it - app works fine without Service Worker, just no offline caching
- **Details**: See TROUBLESHOOTING.md for full guide

**Problem**: "Choose file" button doesn't load images
- **Solution**: Make sure you're granting camera/file permissions when prompted
- Try using "Capture Target" instead
- Check that the file is an image format (JPG, PNG)

**Problem**: Holes not detected
- **Solution**: Adjust "Hole Darkness" slider lower (more sensitive)
- Ensure good photo quality with adequate lighting
- Check that Min/Max Hole Size settings are appropriate

**Problem**: False positives (detecting non-holes)
- **Solution**: Increase "Hole Darkness" threshold
- Increase "Min Hole Size" to filter out small noise
- Use cleaner target sheets

**Problem**: App won't work offline
- **Solution**: Make sure you've installed it as a PWA (Add to Home Screen)
- Visit the app once while online to cache all files
- Check that Service Worker is registered (browser console)

## Data Privacy

- **100% Local**: All data stored on YOUR device only
- **No Cloud**: No data sent to any server
- **No Tracking**: No analytics or tracking scripts
- **Your Control**: Delete all data anytime with "Clear All" button

## Development

### File Structure
```
Bullet-hole-scorer/
├── index.html          # Main app file
├── sw.js              # Service worker for offline functionality
├── manifest.json      # PWA manifest
├── README.md          # This file
└── TROUBLESHOOTING.md # Service worker troubleshooting guide
```

### Customization

To modify detection algorithm, edit these functions in `index.html`:
- `findTargetGridRegion()` - Grid detection
- `detectHolesInTargets()` - Hole detection
- `scoreTargets()` - Scoring logic

### Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Test thoroughly on mobile devices
4. Submit a pull request

## License

MIT License - Free to use, modify, and distribute

## Support

For issues or questions:
- Open a GitHub issue
- Contact: [Your contact info]

## Roadmap

Future enhancements:
- [ ] Export results as PDF/CSV
- [ ] Cloud backup option
- [ ] Multi-shooter comparison
- [ ] Different target sheet formats
- [ ] Shot group analysis
- [ ] Training mode with scoring tips

---

**Made for shooters, by shooters** 🎯

Built to work perfectly offline at any shooting range, no matter how remote!
