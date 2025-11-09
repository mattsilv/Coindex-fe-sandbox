# Requirements Summary - All Components

This document consolidates all user requirements across components for easy reference.

---

## Component 1: Photo Upload

### 1. Flexible Upload Options
1. Support uploading a single coin photo (obverse or reverse)
2. Support uploading multiple coins in one photo (batch upload)
3. Support uploading multiple separate photos in one session
4. Allow mixing of upload types (batch photo + individual close-ups)

### 2. AI Detection
5. AI automatically detects number of coins in each uploaded photo
6. Display detected quantity to user with clear visual indicator
7. AI detection runs after photo upload completes
8. Show "AI detected X coin(s)" message for each photo

### 3. User Quantity Adjustment
9. Provide +/- buttons to adjust detected quantity
10. Minimum quantity is 1 coin per photo
11. No maximum limit on quantity adjustment
12. Changes update in real-time with visual feedback
13. Label clearly states "Quantity: [number] (adjust if needed)"

### 4. Obverse/Reverse Handling
14. Checkbox option: "This photo includes both obverse and reverse sides"
15. Checkbox is optional (unchecked by default)
16. Flexible approach - users not forced to photograph both sides
17. System accommodates partial data (obverse-only or reverse-only photos)

### 5. Privacy Protection (CRITICAL ⚠️)
18. Strip ALL EXIF metadata on client-side BEFORE upload
19. Remove GPS/location data (latitude, longitude, altitude)
20. Remove device information (camera make, model, serial numbers)
21. Remove timestamps (replace with upload timestamp only)
22. Remove software info, user comments, embedded thumbnails
23. Remove camera settings (ISO, aperture, shutter speed, etc.)
24. Preserve ONLY pixel data (image dimensions and visual content)
25. Use HTML5 Canvas API technique for metadata stripping
26. Process at 92% JPEG quality to maintain image clarity
27. Display "Private" badge on all uploaded photos
28. Show privacy notice: "Location & device data removed"
29. Display processing modal: "Removing location & metadata..."
30. Metadata NEVER reaches server - client-side only processing

### 6. Multiple Photo Support
31. Display all uploaded photos in a list/stack view
32. Each photo shows preview thumbnail
33. Each photo has individual remove (X) button
34. "Add Another Photo" button always available after first upload
35. Photos persist in UI until user removes them or continues
36. Photo counter shows total photos uploaded

### 7. User Interface Requirements
37. Mobile-first design (max-width 448px container)
38. Initial state shows camera icon in circle (blue theme)
39. Two upload buttons: "📷 Take Photo" (primary) and "🖼️ Choose from Gallery" (secondary)
40. Primary button has solid blue background
41. Secondary button has blue outline only
42. Tips section with bulleted list explaining features
43. Privacy notice box with green theme and lock icon
44. "Continue to Review" button appears after at least one photo uploaded
45. Continue button shows "AI will analyze your photos" subtitle

### 8. File Handling
46. Accept only image files (image/*)
47. Support camera capture via `capture="environment"` attribute
48. Support gallery selection (no capture attribute)
49. Reset file input after each selection (allows re-selecting same file)
50. Handle file selection errors gracefully

### 9. State Management
51. Track each photo with unique ID
52. Store original file reference (for debugging if needed)
53. Store stripped file for upload
54. Store detected coin quantity per photo
55. Store obverse/reverse checkbox state per photo
56. Store metadata stripped confirmation flag
57. Calculate total coins across all photos

### 10. Next Steps Flow
58. Continue button triggers transition to next component
59. Pass all photos and metadata to next component
60. Show summary: "Processing X photo(s) with Y total coin(s)"
61. Confirm all photos are privacy-protected before proceeding
62. Next component: AI analysis and metadata entry (Component 2)

---

## Component 2: Photo Editor (Future)

### 11. Crop Functionality
63. Basic crop tool for adjusting photo boundaries
64. Should be very simple and intuitive

### 12. Rotate Functionality
65. 90-degree rotation capability
66. Allow multiple rotations (0°, 90°, 180°, 270°)

### 13. Editor Flow
67. Keep as separate component (not combined with upload)
68. Invoked AFTER upload, BEFORE AI analysis
69. Optional step - users can skip if photo is already good

---

## Component 3: AI Analysis & Review (Future)

### 14. AI Results Display
70. Show AI analysis results for each coin
71. AI should attempt to parse out individual coins from batch photos
72. Display confidence scores for AI detections

### 15. User Corrections
73. Allow users to correct AI-detected quantity
74. Allow users to correct AI-detected labels/metadata
75. Make corrections easy and intuitive

### 16. Coin Separation
76. AI should correctly identify number of coin entries needed
77. Users can tweak quantity if AI is wrong
78. Handle both individual and batch photos intelligently

---

## Component 4: Metadata Entry (Future)

### 17. Coin Details Form
79. Year
80. Denomination
81. Grade/condition
82. Country
83. Mint mark
84. Other relevant numismatic data

### 18. Form Behavior
85. Auto-filled from AI analysis where possible
86. Users can edit any field
87. Validation for required fields
88. Save draft functionality

---

## Component 5: Catalog View (Future)

### 19. Display Options
89. Grid view of all uploaded coins
90. Detail view for individual coins
91. Both obverse and reverse photos shown

### 20. Features
92. Search functionality
93. Filter by various criteria
94. Sort options
95. Export capabilities

---

## Cross-Cutting Requirements

### Privacy & Security
96. Never store or transmit location data
97. Never store or transmit device information
98. Client-side processing wherever possible
99. Transparent about data handling
100. GDPR/CCPA compliant by design

### Performance
101. Fast upload processing (under 1 second per photo)
102. Responsive UI (no lag or jank)
103. Works offline where possible
104. Optimized for mobile networks

### User Experience
105. Mobile-first (primary use case)
106. Intuitive UI requiring no instructions
107. Clear visual feedback for all actions
108. Error messages that are helpful, not technical
109. Forgiving of mistakes (easy undo/redo)
110. Progress indicators for long operations

### Accessibility
111. Keyboard navigable
112. Screen reader friendly
113. Sufficient color contrast
114. Touch targets large enough for fingers

---

## Implementation Status

✅ **Complete:** Requirements 1-62 (Component 1: Photo Upload)

⏳ **Pending:** Requirements 63-114 (Future Components)

---

## Priority Order

1. **P0 (Critical):** Requirements 18-30 (Privacy protection)
2. **P1 (High):** Requirements 1-17, 31-62 (Core upload functionality)
3. **P2 (Medium):** Requirements 63-69, 70-78 (Editor and AI review)
4. **P3 (Low):** Requirements 79-95 (Advanced features)
5. **P4 (Nice-to-have):** Requirements 96-114 (Polish and optimization)

---

**Last Updated:** 2025-11-09
**Total Requirements:** 114
**Implemented:** 62 (54%)
**Remaining:** 52 (46%)
