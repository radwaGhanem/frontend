# 📸 How to Replace Emoji Placeholders with Figma Assets

This guide will walk you through replacing all emoji placeholders with your actual design assets from Figma.

## 📋 Table of Contents
1. [Exporting from Figma](#exporting-from-figma)
2. [Organizing Assets](#organizing-assets)
3. [Updating Code](#updating-code)
4. [Quick Reference](#quick-reference)
5. [Troubleshooting](#troubleshooting)

---

## 🎨 Step 1: Exporting from Figma

### For Each Illustration/Icon:

1. **Select the element** in Figma (illustration, icon, etc.)
2. **Right-click** → Select **"Export"** or use the Export panel on the right sidebar
3. **Choose format:**
   - **PNG** - Best for illustrations with transparency (recommended)
   - **SVG** - Best for simple icons (scalable, smaller file size)
   - **JPG** - Only for photos (not recommended for illustrations)

4. **Set export settings:**
   - For mobile apps, export at **2x** or **3x** resolution
   - Example: If design is 200×200px, export at:
     - **2x**: 400×400px (good for most devices)
     - **3x**: 600×600px (for high-resolution displays)

5. **Name your files** descriptively:
   - Use lowercase with hyphens: `onboarding-problem.png`
   - Be consistent with naming

### Export Settings Example:
```
Format: PNG
Size: 2x (or 3x)
Background: Transparent (if needed)
```

---

## 📁 Step 2: Organizing Assets

### Create Folder Structure

Create these folders in your project:

```
assets/images/
├── onboarding/
│   ├── problem.png
│   ├── problem@2x.png      (optional, for retina)
│   ├── problem@3x.png      (optional, for high-res)
│   ├── solution.png
│   └── mission.png
├── auth/
│   ├── lock.png
│   ├── phone.png
│   └── success.png
├── icons/
│   ├── gam3ya.png
│   ├── microloan.png
│   └── startup.png
└── illustrations/
    └── (other illustrations)
```

### Quick Setup Command

Run this in your terminal to create the folders:

```bash
mkdir -p assets/images/onboarding
mkdir -p assets/images/auth
mkdir -p assets/images/icons
mkdir -p assets/images/illustrations
```

---

## 💻 Step 3: Updating Code

The code is already set up to easily switch from emojis to images. Here's how:

### Example 1: Onboarding Screen (`app/onboarding.tsx`)

**Before (using emoji):**
```typescript
const useEmoji = true;
const illustrations: any[] = [];
```

**After (using images):**
```typescript
const useEmoji = false; // Change this to false
const illustrations = [
  require('@/assets/images/onboarding/problem.png'),
  require('@/assets/images/onboarding/solution.png'),
  require('@/assets/images/onboarding/mission.png'),
];
```

### Example 2: Language Screen (`app/language.tsx`)

**Before:**
```typescript
const USE_EMOJI = true;
const PHONE_ILLUSTRATION: any = null;
```

**After:**
```typescript
const USE_EMOJI = false; // Change this to false
const PHONE_ILLUSTRATION = require('@/assets/images/auth/phone.png');
```

### Example 3: Sign In Screen (`app/signin.tsx`)

**Before:**
```typescript
const USE_EMOJI = true;
const LOCK_ILLUSTRATION: any = null;
```

**After:**
```typescript
const USE_EMOJI = false; // Change this to false
const LOCK_ILLUSTRATION = require('@/assets/images/auth/lock.png');
```

---

## 📝 Quick Reference: Files to Update

| File | Emoji Used | Image Path | Status |
|------|-----------|------------|--------|
| `app/onboarding.tsx` | 👩 💼 🚀 | `assets/images/onboarding/problem.png`<br>`assets/images/onboarding/solution.png`<br>`assets/images/onboarding/mission.png` | ⚠️ Needs images |
| `app/language.tsx` | 📱 | `assets/images/auth/phone.png` | ⚠️ Needs image |
| `app/signin.tsx` | 🔒 | `assets/images/auth/lock.png` | ⚠️ Needs image |
| `app/(tabs)/index.tsx` | 📊 🏢 📦 | `assets/images/icons/gam3ya.png`<br>`assets/images/icons/microloan.png`<br>`assets/images/icons/startup.png` | ⚠️ Needs images |
| `app/startup.tsx` | 📄 👥 📚 | Various icons | ⚠️ Needs images |
| `app/gam3ya.tsx` | 👥 | `assets/images/illustrations/gam3ya-circle.png` | ⚠️ Needs image |
| `app/microloan.tsx` | 💵 🆔 💰 | Various icons | ⚠️ Needs images |
| `app/wallet.tsx` | 💳 🏦 | Payment method icons | ⚠️ Needs images |

---

## 🎯 Step-by-Step Checklist

### For Each Screen:

- [ ] Export image from Figma at 2x resolution
- [ ] Save to correct folder (`assets/images/[category]/`)
- [ ] Update the code file:
  - [ ] Change `useEmoji` or `USE_EMOJI` to `false`
  - [ ] Add `require()` statement with correct path
- [ ] Test the screen to verify image appears
- [ ] Check image sizing and adjust if needed

---

## 🛠️ Troubleshooting

### Image Not Showing?

1. **Check file path:**
   ```typescript
   // ✅ Correct
   require('@/assets/images/onboarding/problem.png')
   
   // ❌ Wrong
   require('./assets/images/onboarding/problem.png')
   ```

2. **Clear cache and restart:**
   ```bash
   npm start -- --clear
   ```

3. **Verify file exists:**
   - Check the file is in the correct folder
   - Check file name matches exactly (case-sensitive)

4. **Check file format:**
   - Use PNG for transparency
   - Ensure file isn't corrupted

### Image Too Large/Small?

Adjust the `style` prop in the `Image` component:

```typescript
<Image
  source={illustrations[currentStep]}
  style={{
    width: 200,  // Adjust width
    height: 200, // Adjust height
  }}
  resizeMode="contain"
/>
```

### Performance Issues?

1. **Optimize images:**
   - Use [TinyPNG](https://tinypng.com/) to compress
   - Keep file sizes under 500KB
   - Use appropriate resolution (don't use 3x if 2x is enough)

2. **Use SVG for simple icons:**
   - Install: `npm install react-native-svg`
   - Better for simple graphics

---

## 📐 Recommended Image Sizes

| Type | Design Size | Export Size (2x) | Export Size (3x) |
|------|------------|------------------|------------------|
| Small Icons | 24×24px | 48×48px | 72×72px |
| Medium Icons | 48×48px | 96×96px | 144×144px |
| Illustrations | 200×200px | 400×400px | 600×600px |
| Large Illustrations | 400×400px | 800×800px | 1200×1200px |

---

## ✅ Testing After Adding Images

1. **Start the app:**
   ```bash
   npm start
   ```

2. **Test on device/simulator:**
   - Check images load correctly
   - Verify sizing looks good
   - Test on different screen sizes if possible

3. **Check performance:**
   - Images should load quickly
   - No lag when navigating

---

## 🎨 Pro Tips

1. **Batch Export:** In Figma, select multiple frames and export all at once
2. **Naming Convention:** Use consistent naming (e.g., `screen-element.png`)
3. **Version Control:** Don't commit very large image files (>1MB)
4. **SVG for Icons:** Consider SVG for simple icons (better quality, smaller size)
5. **Asset Catalog:** Keep a list of all assets and their locations

---

## 📞 Need Help?

If you encounter issues:
1. Check the file path is correct
2. Verify the image file isn't corrupted
3. Clear cache and restart: `npm start -- --clear`
4. Check console for error messages

---

**Happy coding! 🚀**
