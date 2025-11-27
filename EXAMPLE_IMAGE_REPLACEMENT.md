# 📸 Example: How to Replace Emoji with Image

This shows exactly what to change in your code.

## Example: Onboarding Screen

### BEFORE (Using Emoji) ❌

```typescript
// app/onboarding.tsx - Lines 24-27

// Temporary: Using emoji until images are added
const useEmoji = true; // Set to false after adding your images
const emojiFallbacks = ['👩', '💼', '🚀'];
const illustrations: any[] = []; // Will be populated when images are added
```

### AFTER (Using Images) ✅

```typescript
// app/onboarding.tsx - Lines 24-27

// Images loaded from assets
const useEmoji = false; // ✅ Changed from true to false
const emojiFallbacks = ['👩', '💼', '🚀']; // Can keep or remove
const illustrations = [
  require('@/assets/images/onboarding/problem.png'),    // ✅ Added
  require('@/assets/images/onboarding/solution.png'),  // ✅ Added
  require('@/assets/images/onboarding/mission.png'),   // ✅ Added
];
```

---

## Visual Comparison

### What You See Now (Emoji):
```
┌─────────────────┐
│                 │
│       👩        │  ← Emoji placeholder
│                 │
└─────────────────┘
```

### What You'll See After (Image):
```
┌─────────────────┐
│                 │
│   [Your Image]  │  ← Your Figma illustration
│                 │
└─────────────────┘
```

---

## Step-by-Step Visual Guide

### Step 1: Export from Figma
```
Figma Design
    ↓
Right-click → Export
    ↓
PNG @ 2x resolution
    ↓
Save as: problem.png
```

### Step 2: Place File
```
Your Computer
    ↓
Copy problem.png
    ↓
Paste into: assets/images/onboarding/
```

### Step 3: Update Code
```
Open: app/onboarding.tsx
    ↓
Find: const useEmoji = true;
    ↓
Change to: const useEmoji = false;
    ↓
Add: require('@/assets/images/onboarding/problem.png')
```

### Step 4: Test
```
npm start -- --clear
    ↓
See your image! 🎉
```

---

## File Structure Example

```
MyApp/
├── assets/
│   └── images/
│       └── onboarding/
│           ├── problem.png      ← Your exported image
│           ├── solution.png      ← Your exported image
│           └── mission.png      ← Your exported image
└── app/
    └── onboarding.tsx           ← File you edit
```

---

## Common Mistakes to Avoid

### ❌ Wrong Path
```typescript
// Don't use relative paths
require('./assets/images/onboarding/problem.png')  // ❌
require('../assets/images/onboarding/problem.png') // ❌
```

### ✅ Correct Path
```typescript
// Use @ alias (points to project root)
require('@/assets/images/onboarding/problem.png')  // ✅
```

### ❌ Forgot to Change Flag
```typescript
const useEmoji = true;  // ❌ Still true!
const illustrations = [require('@/assets/images/onboarding/problem.png')];
// Image won't show because useEmoji is still true
```

### ✅ Correct
```typescript
const useEmoji = false;  // ✅ Changed to false
const illustrations = [require('@/assets/images/onboarding/problem.png')];
// Now image will show!
```

---

## Testing Checklist

After making changes:

- [ ] Image file exists in correct folder
- [ ] `useEmoji` is set to `false`
- [ ] `require()` path is correct (starts with `@/`)
- [ ] Restarted dev server with `--clear` flag
- [ ] Image appears on screen
- [ ] Image size looks correct

---

## Need Help?

If image doesn't show:

1. **Check file path** - Must start with `@/`
2. **Check file exists** - Verify in file explorer
3. **Clear cache** - Run `npm start -- --clear`
4. **Check console** - Look for error messages
5. **Verify format** - File should be PNG

---

**That's it! You're ready to replace all emojis with your beautiful Figma designs! 🎨**

