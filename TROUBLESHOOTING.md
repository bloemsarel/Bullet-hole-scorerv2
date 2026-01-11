# Service Worker Troubleshooting Guide

## Common Issues and Solutions

### ❌ "Service Worker registration failed"

This error appears when the Service Worker can't register. Here are the solutions:

#### Solution 1: Use HTTPS or Localhost
**Service Workers ONLY work on:**
- ✅ HTTPS websites (like GitHub Pages)
- ✅ localhost (http://localhost or http://127.0.0.1)
- ❌ **NOT on file:// protocol** (opening HTML file directly)

**If testing locally:**
```bash
# Option A: Python 3
python -m http.server 8000

# Option B: Python 2
python -m SimpleHTTPServer 8000

# Option C: Node.js
npx http-server

# Then open: http://localhost:8000
```

#### Solution 2: Check Browser Console
1. Open Chrome DevTools (F12)
2. Go to **Console** tab
3. Look for specific error messages
4. Go to **Application** tab → **Service Workers** to see registration status

#### Solution 3: Deploy to GitHub Pages
Service Workers work perfectly on GitHub Pages (uses HTTPS):
1. Push files to your repo
2. Enable GitHub Pages in Settings
3. Visit: `https://yourusername.github.io/Bullet-hole-scorer/`

## Good News: App Works Without Service Worker!

The app is designed to work perfectly even if Service Worker registration fails. You'll just lose:
- Offline caching (need internet on first load)
- "Add to Home Screen" prompt

**All core features still work:**
- ✅ Taking photos
- ✅ Detecting bullet holes
- ✅ Scoring targets
- ✅ Saving results (uses localStorage)
- ✅ Viewing history

## Testing Checklist

### Local Testing
- [ ] Use a local web server (not file://)
- [ ] Check browser console for errors
- [ ] Test in Chrome/Firefox (best support)
- [ ] Check Application → Service Workers tab

### GitHub Pages Testing
- [ ] Files pushed to repo
- [ ] GitHub Pages enabled in settings
- [ ] Visit HTTPS URL
- [ ] Check console on mobile device
- [ ] Try "Add to Home Screen"

## Browser Compatibility

| Browser | Service Worker | PWA Install |
|---------|---------------|-------------|
| Chrome (Android) | ✅ | ✅ |
| Firefox (Android) | ✅ | ✅ |
| Safari (iOS) | ⚠️ Limited | ⚠️ Limited |
| Edge (Android) | ✅ | ✅ |
| Samsung Internet | ✅ | ✅ |

## Verify Service Worker is Working

Open DevTools → Console. You should see:
```
✓ Service Worker registered successfully: https://...
```

If you see a warning instead, the app will still work, just without offline caching.

## Alternative: Standalone HTML Version

If you don't need offline functionality, you can:
1. Remove the service worker registration code
2. Remove `<link rel="manifest">` from HTML
3. Remove `sw.js` and `manifest.json` files
4. App works as a regular webpage

The app saves data to localStorage, so results persist even without a service worker!

## Need Help?

1. Check what error you see in console
2. Verify you're using HTTPS or localhost
3. Try in Chrome on Android (best PWA support)
4. Open a GitHub issue with the specific error message

## Quick Fix: Disable Service Worker

If you want to disable service worker temporarily, comment out this section in index.html:

```javascript
// Service Worker Registration
/* 
if ('serviceWorker' in navigator) {
    // ... comment out all this code
}
*/
```

App will work normally without offline capability.
