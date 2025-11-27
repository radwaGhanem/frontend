# 🚀 API Setup Guide

This guide explains how to configure and use the API integration with your backend.

## ✅ What's Been Set Up

1. **Axios installed** - HTTP client library
2. **API configuration** - Centralized axios instance
3. **Authentication API functions** - Sign in, sign up, password reset
4. **Error handling** - Comprehensive error management
5. **TypeScript types** - Type-safe API calls

## 📁 Files Created

```
services/
├── api.ts          # Axios instance with interceptors
├── authApi.ts      # Authentication API functions
└── README.md        # Detailed API documentation

constants/
└── api.ts          # API configuration constants
```

## 🔧 Configuration Steps

### Step 1: Update API Base URL

Open `constants/api.ts` and update the base URL:

```typescript
export const API_BASE_URL = 'https://your-backend-url.com/api';
```

**Or use environment variables:**

1. Create a `.env` file in the root directory:
```env
EXPO_PUBLIC_API_URL=https://your-backend-url.com/api
```

2. The code will automatically use this value.

### Step 2: Update API Endpoints (if needed)

If your backend uses different endpoint paths, update them in `constants/api.ts`:

```typescript
export const API_ENDPOINTS = {
  AUTH: {
    SIGNIN: '/auth/signin',    // Your actual endpoint
    SIGNUP: '/auth/signup',     // Your actual endpoint
    // ...
  },
};
```

### Step 3: Update Request/Response Format (if needed)

If your backend uses a different response format, update the types in `services/authApi.ts`:

**Current expected format:**
```json
{
  "success": true,
  "message": "Success message",
  "data": {
    "token": "jwt-token-here",
    "user": {
      "id": "user-id",
      "email": "user@example.com",
      "name": "User Name"
    }
  }
}
```

**Update the `SignInResponse` and `SignUpResponse` interfaces if different.**

## 📝 How It Works

### Sign In Flow

1. User enters email/phone and password
2. `handleSignIn()` is called
3. API determines if input is email or phone
4. POST request sent to `/auth/signin`
5. On success: Token saved, user navigated to dashboard
6. On error: Error message displayed

### Sign Up Flow

1. User fills registration form
2. Form validation runs
3. `handleSignUp()` is called
4. POST request sent to `/auth/signup`
5. On success: Token saved, user navigated to profile setup
6. On error: Error message displayed

## 🔐 Adding Token Storage

To automatically include auth tokens in API requests:

1. Install AsyncStorage:
```bash
npm install @react-native-async-storage/async-storage
```

2. Update `services/api.ts`:

```typescript
import AsyncStorage from '@react-native-async-storage/async-storage';

api.interceptors.request.use(
  async (config) => {
    const token = await AsyncStorage.getItem('authToken');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);
```

3. Update sign in/sign up to save token:

```typescript
// In app/signin.tsx and app/signup.tsx
import AsyncStorage from '@react-native-async-storage/async-storage';

// After successful API call:
await AsyncStorage.setItem('authToken', response.data.token);
await AsyncStorage.setItem('user', JSON.stringify(response.data.user));
```

## 🧪 Testing

### Test Sign In

1. Make sure backend is running
2. Update API URL in `constants/api.ts`
3. Open app and go to Sign In screen
4. Enter credentials
5. Check:
   - Network tab for request
   - Console for errors
   - App navigation on success

### Test Sign Up

1. Go to Sign Up screen
2. Fill all fields
3. Submit form
4. Verify API call is made

## 🐛 Troubleshooting

### "Network Error" or "Request failed"

- Check API URL is correct
- Verify backend is running
- Check CORS settings on backend
- Verify network connectivity

### "401 Unauthorized"

- Check credentials are correct
- Verify backend authentication logic
- Check token format if using tokens

### "404 Not Found"

- Verify endpoint paths in `constants/api.ts`
- Check backend route definitions

### Type Errors

- Make sure TypeScript types match your backend response
- Update interfaces in `services/authApi.ts` if needed

## 📋 Backend Requirements

Your backend should:

1. **Accept POST requests** to `/auth/signin` and `/auth/signup`
2. **Return JSON responses** in the expected format
3. **Handle CORS** for mobile app requests
4. **Validate inputs** and return appropriate error messages
5. **Return tokens** on successful authentication

### Example Backend Endpoint (Node.js/Express)

```javascript
app.post('/api/auth/signin', async (req, res) => {
  const { email, phone, password } = req.body;
  
  // Validate and authenticate
  const user = await authenticateUser(email || phone, password);
  
  if (user) {
    const token = generateToken(user);
    res.json({
      success: true,
      message: 'Sign in successful',
      data: {
        token,
        user: {
          id: user.id,
          email: user.email,
          name: user.name,
        },
      },
    });
  } else {
    res.status(401).json({
      success: false,
      message: 'Invalid credentials',
    });
  }
});
```

## 🎯 Next Steps

1. ✅ Update API URL
2. ✅ Test sign in endpoint
3. ✅ Test sign up endpoint
4. ✅ Add token storage (AsyncStorage)
5. ✅ Add token to request headers
6. ✅ Test protected endpoints

## 📚 Additional Resources

- See `services/README.md` for detailed API documentation
- See `services/authApi.ts` for all available functions
- See `constants/api.ts` for configuration options

---

**Your API integration is ready! Just update the URL and start testing! 🎉**

