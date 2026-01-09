# Security & Best Practices

## API Key Management

### Leaked Google Maps API Key - Resolution

**Issue**: A Google Maps API key was detected in the repository history by GitHub's secret scanning.

**Resolution**:
1. ✅ The key has been revoked (not usable anymore)
2. ✅ A new `.env.example` file has been added with instructions
3. ✅ `.gitignore` is configured to exclude `.env` files

### How to Use the Google Maps API Securely

#### Option 1: Environment Variables (Recommended for build processes)
1. Copy `.env.example` to `.env` (`.env` is in `.gitignore` and won't be committed)
2. Add your Google Maps API key:
   ```
   GOOGLE_MAPS_API_KEY=your_actual_key_here
   ```
3. Use a build tool (Webpack, Parcel, Vite) to inject this at build time

#### Option 2: Runtime Injection (For static sites)
1. Load the key from a secure backend endpoint
2. Call the API from your server, not from client-side code
3. Or use the Maps Embed API with restricted keys instead of the JavaScript API

#### Option 3: API Key Restrictions (For public usage)
If you must embed the key in HTML:
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Set **Restrictions** on your API key:
   - **Application restrictions**: HTTP referrers → add your domain(s)
   - **API restrictions**: Restrict to only Maps JavaScript API
3. Monitor usage regularly for unauthorized access

### Prevention for Future Commits

- Never commit `.env` files (already in `.gitignore`)
- Rotate API keys regularly
- Use GitHub's secret scanning to detect accidental leaks
- Consider using GitHub Secrets for CI/CD deployments
- Run `git log -p -S "AIza"` periodically to check for accidental key commits

### Reporting Additional Security Issues

If you find a security issue:
1. **DO NOT** open a public issue on GitHub
2. Email the maintainer privately
3. Follow responsible disclosure practices
4. Allow time for fixes before public disclosure
