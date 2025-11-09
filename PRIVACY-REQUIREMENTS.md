# Privacy Requirements: Client-Side Metadata Stripping

## Critical Privacy Feature

**All personally identifiable metadata MUST be stripped from photos on the client-side BEFORE upload.**

## What Gets Removed

The following EXIF metadata must be removed from all uploaded photos:

- **GPS/Location data** - Latitude, longitude, altitude
- **Device information** - Camera make, model, serial numbers
- **Timestamps** - Original capture date/time (new timestamp is added)
- **Software info** - Editing software, firmware versions
- **User comments** - Any embedded text or descriptions
- **Thumbnail images** - Embedded preview images
- **Camera settings** - ISO, aperture, shutter speed, etc.

## What Gets Preserved

Only the pixel data (the actual image) is preserved:
- Image width and height
- Color information
- Visual content

## Implementation Details

### Client-Side Processing

The metadata stripping happens in the browser using HTML5 Canvas API:

```javascript
async function stripMetadata(file) {
    return new Promise((resolve, reject) => {
        const img = new Image();
        const reader = new FileReader();

        reader.onload = function(e) {
            img.onload = function() {
                // Create canvas and draw image (this strips EXIF)
                const canvas = document.createElement('canvas');
                canvas.width = img.width;
                canvas.height = img.height;
                const ctx = canvas.getContext('2d');
                ctx.drawImage(img, 0, 0);

                // Convert to blob (JPEG with no metadata)
                canvas.toBlob(function(blob) {
                    const strippedFile = new File([blob], file.name, {
                        type: 'image/jpeg',
                        lastModified: Date.now()
                    });
                    resolve(strippedFile);
                }, 'image/jpeg', 0.92); // 92% quality to preserve clarity
            };
            img.onerror = reject;
            img.src = e.target.result;
        };
        reader.onerror = reject;
        reader.readAsDataURL(file);
    });
}
```

### Why Client-Side?

1. **Trust Model**: Metadata never reaches our servers - impossible for us to access
2. **Privacy by Design**: Users don't have to trust us - the code runs in their browser
3. **Legal Compliance**: Reduces liability - we never possess PII from photos
4. **User Control**: Users can verify via browser DevTools if desired

### User Experience

1. User selects photo
2. Brief "Processing Photo - Removing location & metadata..." modal shown
3. Original file is processed in-memory
4. Stripped version is uploaded
5. "Private" badge shown on uploaded photos
6. Privacy notice displayed in UI

### Quality Preservation

- JPEG quality set to 92% to balance file size and image clarity
- Maintains original dimensions
- No visual degradation for coin identification purposes

### Production Considerations

For production implementation:

1. **Consider using a library** like `browser-image-compression` for better compression
2. **Add file size limits** (e.g., 10MB max)
3. **Verify stripping** - could add automated tests to ensure no EXIF remains
4. **Handle edge cases** - HEIC/HEIF formats from iOS, WebP, etc.
5. **Add fallback** - If canvas API fails, show warning to user
6. **Audit trail** - Log on server that client claimed to strip metadata (but never trust it)

### Security Notes

- **Never trust client-side only** - Treat as defense-in-depth
- **Server-side verification** - Could add server-side EXIF check as secondary measure
- **Transparency** - Make this feature prominent in privacy policy
- **Open source option** - Consider making stripping code auditable

### Testing

To verify metadata stripping works:

1. Take photo with GPS enabled
2. Upload via the app
3. Download uploaded image
4. Check EXIF with tool like `exiftool`:
   ```bash
   exiftool downloaded-photo.jpg
   ```
5. Should see no GPS, device, or sensitive metadata

### Alternative Approaches Considered

1. **Server-side stripping** - Rejected because metadata reaches server
2. **Native app only** - Web can do this too with Canvas API
3. **User opt-in** - Made mandatory because privacy should be default

## UI/UX Considerations

### Visual Indicators

- 🔒 Privacy badge in header: "Location & device data removed"
- 🔒 "Private" badge on each uploaded photo
- 🔒 Green privacy notice box explaining the feature
- Loading modal during processing

### Messaging

Clear, non-technical language:
- ✅ "Location & device data removed"
- ❌ "EXIF metadata stripped" (too technical)

### Performance

- Processing adds ~200-500ms per photo
- Worth the tradeoff for privacy guarantee
- Could optimize with Web Workers for large batches

## Compliance Benefits

This approach helps with:

- **GDPR** - Minimizes personal data collection
- **CCPA** - Reduces data privacy obligations
- **General privacy best practices**
- **User trust** - Demonstrates privacy commitment

## Questions for Product Team

1. Should we allow users to opt-out? (Recommendation: No, make it mandatory)
2. Do we want to support RAW formats? (These can be large, may need different approach)
3. Should we add a "View technical details" button showing what was removed?
4. Do we need to preserve orientation EXIF? (Currently stripped, could preserve if needed)

## Documentation for Users

Suggested privacy policy language:

> "All photos are automatically processed in your browser before upload to remove location data, device information, and other metadata. Only the image itself is sent to our servers. This happens on your device and cannot be disabled - your privacy is our priority."
