# 🎯 Target Scorer v3.0

Professional bullet hole detection and scoring system for .22 caliber shooting targets.

## ✨ Features

- **Accurate mm-based scoring** matching official competition rules
- **Proper X-ring detection** accounting for bullet hole size (2.5mm radius)
- **Mobile camera support** - take photos directly from your phone
- **Smart hole detection** - distinguishes bullet holes from printed circles
- **Save & track results** - history stored locally in your browser
- **Works offline** - no internet needed after loading

## 📱 Installation

### For GitHub Pages:

1. Go to your repository: `bloemsarel.github.io/Bullet-hole-scorerv2`
2. Upload or replace with `index.html` (the target-scorer-v3.html file)
3. Wait a few minutes for GitHub Pages to update
4. Visit: `https://bloemsarel.github.io/Bullet-hole-scorerv2/`

### File Structure:
```
Bullet-hole-scorerv2/
├── index.html          (the main app - only file you need!)
└── README.md           (this file - optional)
```

## 🎯 Scoring Rules

The app follows official .22 caliber target scoring:

| Zone | Radius | Score | Notes |
|------|--------|-------|-------|
| X-ring | 0.5mm | 10+X | Tie-breaker (accounts for 2.5mm bullet hole) |
| Ring 2 | 6mm | 10 | |
| Ring 3 | 9mm | 9 | |
| Ring 4 | 12mm | 8 | |
| Ring 5 | 15mm | 7 | |
| Ring 6 | 18mm | 6 | |
| Ring 7 | 21mm | 5 | |
| Ring 8 | 24mm | 4 | |

**Important Rule:** When a bullet hole touches or crosses a circle line from the inside, it scores the higher value (the smaller circle's score).

## 📸 How to Use

1. **Take Photo or Select Image**
   - Mobile: Tap "📸 TAKE PHOTO" to open camera
   - Desktop: Tap "📁 SELECT IMAGE" to browse files

2. **Automatic Processing**
   - App detects 25 targets in 5x5 grid
   - Finds bullet holes using advanced image analysis
   - Calculates scores based on exact mm measurements

3. **View Results**
   - Total score, X-rings, and statistics
   - Individual target breakdown
   - Annotated image showing detected holes

4. **Save Results**
   - Optional: Enter shooter ID
   - Tap "💾 SAVE RESULTS"
   - View saved results anytime

## 🔧 Technical Details

- **Hole Detection:** 
  - Darkness threshold: 35 (distinguishes holes from printed circles)
  - Solidity check: ≥65% (holes are filled, circles are hollow)
  - Size filter: 8-600 pixels
  - Aspect ratio: 0.25-4.0 (roughly circular)

- **Calibration:**
  - Target diameter: 48mm (24mm radius × 2)
  - Target occupies 82% of cell width
  - Accurate pixel-to-mm conversion

- **X-ring Logic:**
  - Bullet hole radius: 2.5mm
  - X-ring radius: 0.5mm
  - X scored when hole EDGE is within 0.5mm of center
  - Center can be up to 3mm away (0.5 + 2.5)

## 🐛 Troubleshooting

**Camera not working?**
- Make sure you're using HTTPS (GitHub Pages uses HTTPS automatically)
- Grant camera permissions when prompted
- Try "📁 SELECT IMAGE" instead if camera fails

**Scoring seems wrong?**
- Ensure good lighting when photographing targets
- Target should be flat and well-lit
- Avoid shadows and glare
- Make sure all 25 targets are visible in the image

**Holes not detected?**
- Bullet holes must be darker than printed circles
- Minimum hole size: 8 pixels
- Maximum hole size: 600 pixels
- Check debug panel for detection info

## 📊 Version History

### v3.0 (Current)
- ✅ Fixed camera input (label-based approach)
- ✅ Proper mm-based scoring matching Python script
- ✅ Improved hole detection algorithm
- ✅ Better mobile support
- ✅ Debug panel for troubleshooting

### v2.0
- Corrected scoring zones
- X-ring detection with bullet size compensation

### v1.0
- Initial release
- Basic hole detection

## 📄 License

Free to use for personal and competition purposes.

## 🤝 Credits

Scoring algorithm based on official .22 caliber target shooting rules.

---

**Questions or Issues?** Check the debug panel (green/red text) for real-time status updates.
