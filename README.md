# Coindex Frontend Sandbox

Frontend experimentation repository for the Coindex coin photography and cataloging app.

## 🎯 Project Goal

Build a mobile-first web app for coin collectors to:
1. Upload photos of their coins (single or batch)
2. Use AI to automatically detect and identify coins
3. Review and edit coin metadata
4. Build a digital coin catalog

## 🚀 Current Status

**Phase 1: Photo Upload Component** ✅ Complete

Live demo: https://mattsilv.github.io/Coindex-fe-sandbox/

### Implemented Features
- ✅ Flexible upload (single coin or multiple coins per photo)
- ✅ AI coin detection simulation (1-3 coins per photo)
- ✅ Quantity adjustment controls (+/- buttons)
- ✅ Multiple photo upload support
- ✅ Client-side metadata stripping for privacy
- ✅ "Private" badges and privacy notices
- ✅ Mobile-first responsive design
- ✅ Tips and user guidance

### Next Components (Not Yet Built)
- ⏳ Photo Editor (crop/rotate)
- ⏳ AI Analysis & Coin Review
- ⏳ Metadata Entry Form
- ⏳ Coin Catalog View

## 📁 Repository Structure

```
Coindex-fe-sandbox/
├── index.html                  # Photo upload component (live)
├── photo-capture-mockup.html   # Original mockup (for reference)
├── README.md                   # This file
├── COMPONENT-01-UPLOAD.md      # Upload component specification
├── PRIVACY-REQUIREMENTS.md     # Privacy feature technical docs
└── .git/
```

## 📋 Component Documentation

### Component 1: Photo Upload
**File:** `COMPONENT-01-UPLOAD.md`

**Key Requirements:**
1. Flexible upload options (single/batch)
2. AI coin detection
3. User quantity adjustment
4. Obverse/reverse handling
5. **Privacy protection** (metadata stripping)
6. Multiple photo support
7. Mobile-first UI
8. File handling
9. State management
10. Next steps flow

See full documentation: [COMPONENT-01-UPLOAD.md](./COMPONENT-01-UPLOAD.md)

### Privacy Feature
**File:** `PRIVACY-REQUIREMENTS.md`

**Critical requirement:** All GPS, device info, and metadata stripped client-side BEFORE upload.

- Uses HTML5 Canvas API
- Removes EXIF data completely
- Only pixel data preserved
- Privacy by design (not policy)

See full documentation: [PRIVACY-REQUIREMENTS.md](./PRIVACY-REQUIREMENTS.md)

## 🛠️ Tech Stack

- **Frontend:** Pure HTML + Tailwind CSS (via CDN)
- **JavaScript:** Vanilla ES6+
- **Deployment:** GitHub Pages
- **No build step** - Rapid iteration for wireframing

### Why This Stack?

This is a **sandbox for rapid wireframing**. We're using the simplest possible setup:
- No framework overhead
- No npm dependencies
- No build process
- Just edit HTML and refresh browser

**Production stack will be different** (likely Next.js + Cloudflare Workers based on engineering handoff docs).

## 🚦 Getting Started

### View Live Demo
https://mattsilv.github.io/Coindex-fe-sandbox/

### Run Locally
```bash
# Clone the repo
git clone https://github.com/mattsilv/Coindex-fe-sandbox.git
cd Coindex-fe-sandbox

# Open in browser
open index.html
# or just double-click index.html
```

No server needed - it's just HTML!

### Iterate on Design
1. Edit `index.html`
2. Refresh browser
3. Push to GitHub
4. GitHub Pages auto-deploys in ~1 minute

## 📱 Testing

### Browser Compatibility
Test on:
- ✅ iOS Safari (primary target)
- ✅ Android Chrome
- ✅ Desktop Chrome (dev only)

### Test Scenarios
1. Upload single coin photo
2. Upload photo with multiple coins
3. Upload multiple separate photos
4. Adjust quantities
5. Check privacy badge appears
6. Verify metadata is stripped

### Privacy Verification
```bash
# Upload a photo via the app
# Download it from server (once backend exists)
# Check EXIF metadata:
exiftool downloaded-photo.jpg

# Should show NO GPS, device, or personal data
```

## 🔒 Privacy First

**ALL photos have metadata stripped before upload.**

- GPS/location removed
- Device info removed
- Timestamps removed
- Only pixel data preserved
- Processing happens in user's browser
- Metadata NEVER reaches server

See [PRIVACY-REQUIREMENTS.md](./PRIVACY-REQUIREMENTS.md) for technical details.

## 📝 Development Workflow

### Branch Strategy
- `main` - Stable, deployable code
- `claude/[feature]-[session-id]` - Active development branches
- `gh-pages` - GitHub Pages deployment (auto-managed)

### Commit Messages
Follow conventional commits:
```
feat: add photo upload component
fix: correct metadata stripping on iOS
docs: add component specification
```

### Deployment
Push to `main` branch:
```bash
git add .
git commit -m "Your message"
git push origin main
```

GitHub Pages deploys automatically.

## 🎨 Design System

### Colors
- **Primary:** Blue (#2563eb)
- **Secondary:** Purple (#9333ea)
- **Success:** Green (#16a34a)
- **Danger:** Red (#dc2626)

### Typography
- **Headings:** font-semibold, text-lg or text-xl
- **Body:** text-sm or text-base
- **Labels:** text-xs

### Spacing
- **Container:** max-w-md (448px)
- **Padding:** p-4 or p-6
- **Gaps:** gap-2, gap-3, gap-4

### Components
- **Buttons:** rounded-lg, px-6 py-3
- **Icons:** w-5 h-5 (buttons), w-4 h-4 (inline)
- **Cards:** rounded-lg shadow-lg

## 🔮 Roadmap

### Phase 1: Photo Upload ✅ Complete
- [x] Upload UI
- [x] Multiple photos
- [x] Privacy protection
- [x] AI detection simulation

### Phase 2: Photo Editing (Next)
- [ ] Crop tool
- [ ] Rotate (90° increments)
- [ ] Basic adjustments
- [ ] Preview mode

### Phase 3: AI Analysis
- [ ] Real AI integration
- [ ] Coin detection
- [ ] Text extraction (dates, denominations)
- [ ] Confidence scores

### Phase 4: Metadata Entry
- [ ] Auto-filled form from AI
- [ ] Manual corrections
- [ ] Validation
- [ ] Save to database

### Phase 5: Catalog View
- [ ] Grid view of all coins
- [ ] Detail view
- [ ] Search/filter
- [ ] Export options

## 🤝 Contributing

This is a personal sandbox repo for rapid wireframing.

If you're working on implementation:
1. Read component docs in `COMPONENT-*.md` files
2. Check requirements are numbered for easy reference
3. Privacy requirements are CRITICAL - must implement
4. Test on mobile first

## 📄 License

Private repository - all rights reserved.

## 📞 Contact

Questions? Open an issue or contact repo owner.

---

**Last Updated:** 2025-11-09
**Current Phase:** Photo Upload Component (Complete)
**Next Phase:** Photo Editor Component
