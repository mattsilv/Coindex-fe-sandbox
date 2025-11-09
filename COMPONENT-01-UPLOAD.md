# Component 1: Photo Upload Component

## Overview
Flexible photo upload system that allows users to upload individual coins or multiple coins in a single photo, with AI-assisted detection and client-side privacy protection.

## Requirements

### 1. Flexible Upload Options
- **1.1** Support uploading a single coin photo (obverse or reverse)
- **1.2** Support uploading multiple coins in one photo (batch upload)
- **1.3** Support uploading multiple separate photos in one session
- **1.4** Allow mixing of upload types (e.g., batch photo + individual close-ups)

### 2. AI Detection
- **2.1** AI automatically detects number of coins in each uploaded photo
- **2.2** Display detected quantity to user with clear visual indicator
- **2.3** AI detection runs after photo upload completes
- **2.4** Show "AI detected X coin(s)" message for each photo

### 3. User Quantity Adjustment
- **3.1** Provide +/- buttons to adjust detected quantity
- **3.2** Minimum quantity is 1 coin per photo
- **3.3** No maximum limit on quantity adjustment
- **3.4** Changes update in real-time with visual feedback
- **3.5** Label clearly states "Quantity: [number] (adjust if needed)"

### 4. Obverse/Reverse Handling
- **4.1** Checkbox option: "This photo includes both obverse and reverse sides"
- **4.2** Checkbox is optional (unchecked by default)
- **4.3** Flexible approach - users not forced to photograph both sides
- **4.4** System accommodates partial data (obverse-only or reverse-only photos)

### 5. Privacy Protection (CRITICAL)
- **5.1** Strip ALL EXIF metadata on client-side BEFORE upload
- **5.2** Remove GPS/location data (latitude, longitude, altitude)
- **5.3** Remove device information (camera make, model, serial numbers)
- **5.4** Remove timestamps (replace with upload timestamp only)
- **5.5** Remove software info, user comments, embedded thumbnails
- **5.6** Remove camera settings (ISO, aperture, shutter speed, etc.)
- **5.7** Preserve ONLY pixel data (image dimensions and visual content)
- **5.8** Use HTML5 Canvas API technique for metadata stripping
- **5.9** Process at 92% JPEG quality to maintain image clarity
- **5.10** Display "Private" badge on all uploaded photos
- **5.11** Show privacy notice: "Location & device data removed"
- **5.12** Display processing modal: "Removing location & metadata..."
- **5.13** Metadata NEVER reaches server - client-side only processing

### 6. Multiple Photo Support
- **6.1** Display all uploaded photos in a list/stack view
- **6.2** Each photo shows preview thumbnail
- **6.3** Each photo has individual remove (X) button
- **6.4** "Add Another Photo" button always available after first upload
- **6.5** Photos persist in UI until user removes them or continues
- **6.6** Photo counter shows total photos uploaded

### 7. User Interface Requirements
- **7.1** Mobile-first design (max-width 448px container)
- **7.2** Initial state shows camera icon in circle (blue theme)
- **7.3** Two upload buttons: "📷 Take Photo" (primary) and "🖼️ Choose from Gallery" (secondary)
- **7.4** Primary button has solid blue background
- **7.5** Secondary button has blue outline only
- **7.6** Tips section with bulleted list explaining features
- **7.7** Privacy notice box with green theme and lock icon
- **7.8** "Continue to Review" button appears after at least one photo uploaded
- **7.9** Continue button shows "AI will analyze your photos" subtitle

### 8. File Handling
- **8.1** Accept only image files (image/*)
- **8.2** Support camera capture via `capture="environment"` attribute
- **8.3** Support gallery selection (no capture attribute)
- **8.4** Reset file input after each selection (allows re-selecting same file)
- **8.5** Handle file selection errors gracefully

### 9. State Management
- **9.1** Track each photo with unique ID
- **9.2** Store original file reference (for debugging if needed)
- **9.3** Store stripped file for upload
- **9.4** Store detected coin quantity per photo
- **9.5** Store obverse/reverse checkbox state per photo
- **9.6** Store metadata stripped confirmation flag
- **9.7** Calculate total coins across all photos

### 10. Next Steps Flow
- **10.1** Continue button triggers transition to next component
- **10.2** Pass all photos and metadata to next component
- **10.3** Show summary: "Processing X photo(s) with Y total coin(s)"
- **10.4** Confirm all photos are privacy-protected before proceeding
- **10.5** Next component: AI analysis and metadata entry (Component 2)

## Technical Implementation

### File Structure
```
index.html              # Main upload component (current implementation)
PRIVACY-REQUIREMENTS.md # Privacy feature technical documentation
COMPONENT-01-UPLOAD.md  # This file
```

### Key Functions
- `handleFileSelect(event)` - Process file selection
- `stripMetadata(file)` - Remove EXIF data from image
- `addPhotoToList(photoId, imageUrl, filename)` - Add photo to UI
- `adjustQuantity(photoId, delta)` - Adjust coin quantity
- `removePhoto(photoId)` - Remove photo from list
- `updateUI()` - Toggle between initial and preview states
- `handleContinue()` - Proceed to next step

### Data Structure
```javascript
{
  id: "photo-1",
  file: File,              // Stripped file for upload
  originalFile: File,      // Original with metadata (not uploaded)
  detectedCoins: Number,   // AI detected quantity
  metadataStripped: Boolean // Confirmation flag
}
```

## Future Enhancements (Not Yet Implemented)

### Component 2: Photo Editor (Crop/Rotate)
- Basic crop functionality
- 90-degree rotation
- Should be separate component
- Invoked AFTER upload, BEFORE AI analysis

### Component 3: Coin Review & Metadata Entry
- Display AI analysis results
- Allow users to correct/edit AI predictions
- Enter coin details (year, denomination, grade, etc.)
- Preview mode before final submission

## Testing Checklist

- [ ] Upload single coin photo
- [ ] Upload photo with multiple coins
- [ ] Upload multiple separate photos
- [ ] Adjust quantity with +/- buttons
- [ ] Remove photo with X button
- [ ] Check "both sides" checkbox
- [ ] Verify "Private" badge appears
- [ ] Verify metadata is stripped (use exiftool on downloaded image)
- [ ] Test on iOS Safari
- [ ] Test on Android Chrome
- [ ] Test on desktop Chrome
- [ ] Test camera capture vs gallery selection
- [ ] Test with large image files
- [ ] Test with portrait vs landscape images
- [ ] Verify Continue button appears/disappears correctly
- [ ] Verify photo counter updates correctly

## Deployment

Current deployment: **GitHub Pages**
- URL: https://mattsilv.github.io/Coindex-fe-sandbox/
- Branch: `claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza` (or `main` after merge)
- Auto-deploys on push to configured branch

## Questions / Decisions Needed

1. **Image compression** - Currently 92% JPEG quality. Adjust?
2. **File size limits** - Should we enforce max file size (e.g., 10MB)?
3. **Multiple file selection** - Support `<input multiple>`?
4. **Image format support** - Handle HEIC/HEIF from iOS?
5. **Orientation EXIF** - Currently stripped. Should we preserve for proper rotation?
6. **Batch processing UI** - Show progress bar for multiple photos?
7. **Error handling** - What to show if Canvas API fails?
8. **Server-side validation** - Double-check metadata removal on server?

## Privacy & Compliance Notes

- **GDPR Compliant** - Minimizes personal data collection
- **CCPA Compliant** - Reduces data privacy obligations
- **Transparency** - Feature prominently displayed to users
- **Trust Model** - Users don't have to trust us - code runs in their browser
- **Legal Protection** - We never possess location/device PII from photos

See `PRIVACY-REQUIREMENTS.md` for complete privacy feature documentation.
