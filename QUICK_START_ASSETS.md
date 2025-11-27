# 🚀 Quick Start: Replace Emojis with Images

## The Fastest Way

### 1. Export from Figma
- Select your illustration/icon
- Right-click → Export → PNG
- Choose **2x** resolution
- Save with a descriptive name

### 2. Place in Project
Put images in these folders:
- `assets/images/onboarding/` - For onboarding screens
- `assets/images/auth/` - For login/signup screens  
- `assets/images/icons/` - For small icons
- `assets/images/illustrations/` - For other illustrations

### 3. Update Code (3 Simple Steps)

#### For Onboarding (`app/onboarding.tsx`):
```typescript
// Find this line (around line 25):
const useEmoji = true;

// Change to:
const useEmoji = false;

// Then add these lines right after (around line 27):
const illustrations = [
  require('@/assets/images/onboarding/problem.png'),
  require('@/assets/images/onboarding/solution.png'),
  require('@/assets/images/onboarding/mission.png'),
];
```

#### For Language Screen (`app/language.tsx`):
```typescript
// Find this line (around line 16):
const USE_EMOJI = true;

// Change to:
const USE_EMOJI = false;

// Then add this line right after:
const PHONE_ILLUSTRATION = require('@/assets/images/auth/phone.png');
```

#### For Sign In (`app/signin.tsx`):
```typescript
// Find this line (around line 19):
const USE_EMOJI = true;

// Change to:
const USE_EMOJI = false;

// Then add this line right after:
const LOCK_ILLUSTRATION = require('@/assets/images/auth/lock.png');
```

### 4. Test
```bash
npm start -- --clear
```

That's it! 🎉

---

## 📋 Complete Checklist

### Priority 1 (Most Visible):
- [ ] Onboarding illustrations (3 images)
- [ ] Language screen phone illustration
- [ ] Sign in lock illustration

### Priority 2:
- [ ] Dashboard quick action icons (Gam3ya, Microloan, Startup)
- [ ] Wallet payment method icons
- [ ] Other screen icons

---

## 💡 Pro Tip

You can do this one screen at a time! Start with the onboarding screen since users see it first.

For detailed instructions, see `ASSETS_GUIDE.md`
