# Netlify Deployment Guide

## Environment Variables Setup

### Required Environment Variables

In your Netlify dashboard, go to **Site settings > Environment variables** and add:

1. **OPENAI_API_KEY**
   - Value: Your OpenAI API key (starts with `sk-`)
   - Used for: OpenAI GPT model access

2. **ANTHROPIC_API_KEY** (Optional)
   - Value: Your Anthropic API key
   - Used for: Claude model access

### Setting Environment Variables

1. **Log into your Netlify dashboard**
2. **Navigate to your site**
3. **Go to Site settings > Environment variables**
4. **Click "Add a variable"**
5. **Add OPENAI_API_KEY:**
   - Key: `OPENAI_API_KEY` (exactly as shown, case-sensitive)
   - Value: Your OpenAI API key (starts with `sk-`)
   - Scopes: Leave as "All scopes" (default)
6. **Add ANTHROPIC_API_KEY (optional):**
   - Key: `ANTHROPIC_API_KEY` (exactly as shown, case-sensitive)  
   - Value: Your Anthropic API key
   - Scopes: Leave as "All scopes" (default)
7. **Click "Save"**
8. **Important: Trigger a new deploy**
   - Go to "Deploys" tab
   - Click "Trigger deploy" > "Deploy site"
   - Environment variables only take effect after a new deployment

## Deployment Steps

### Option 1: Git Integration (Recommended)

1. **Connect Repository**
   ```bash
   # Push your code to GitHub
   git add .
   git commit -m "Add Netlify serverless functions"
   git push origin main
   ```

2. **Deploy from Netlify Dashboard**
   - Go to Netlify dashboard
   - Click "New site from Git"
   - Connect your GitHub repository
   - Set build settings:
     - **Build command**: `echo 'No build step required'`
     - **Publish directory**: `.` (root directory)
   - Deploy site

### Option 2: Netlify CLI

1. **Install Netlify CLI**
   ```bash
   npm install -g netlify-cli
   ```

2. **Login to Netlify**
   ```bash
   netlify login
   ```

3. **Initialize Site**
   ```bash
   netlify init
   ```

4. **Deploy**
   ```bash
   # Deploy to preview
   netlify deploy
   
   # Deploy to production
   netlify deploy --prod
   ```

## Local Development

### Setup
```bash
# Install dependencies
npm install

# Start local development server
netlify dev
```

This will:
- Start the site on `http://localhost:8888`
- Enable serverless functions at `/.netlify/functions/`
- Load environment variables from `.env` file (create one for local development)

### Local Environment Variables

Create a `.env` file in the root directory:
```
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
```

**Note**: Never commit the `.env` file to version control.

## How It Works

### Development Mode
- Users can enter their own API keys
- Direct API calls to OpenAI/Anthropic
- Full functionality for testing

### Production Mode
- No API keys required from users
- Uses Netlify serverless functions
- API keys stored securely as environment variables
- Automatic fallback when no user API key is provided

### Serverless Functions

The deployment includes two serverless functions:

1. **`/.netlify/functions/openai-chat`**
   - Handles OpenAI API requests
   - Uses `OPENAI_API_KEY` environment variable

2. **`/.netlify/functions/anthropic-chat`**
   - Handles Anthropic API requests  
   - Uses `ANTHROPIC_API_KEY` environment variable

### Security Features

- API keys never exposed to client-side code
- CORS headers properly configured
- Error handling for missing environment variables
- Request validation and sanitization

## Troubleshooting

### Environment Variables Not Loading

1. **Check Environment Variable Names**
   - Must be exactly: `OPENAI_API_KEY` (case-sensitive)
   - Must be exactly: `ANTHROPIC_API_KEY` (case-sensitive)

2. **Verify in Netlify Dashboard**
   - Go to Site settings > Environment variables
   - Ensure variables are set for "All scopes" or "All deploy contexts"
   - Click "Edit" to verify the values are correct

3. **Test Environment Variables**
   ```bash
   # Test the environment check function
   curl https://your-site.netlify.app/.netlify/functions/test-env
   ```

4. **Redeploy After Adding Variables**
   - Environment variables only take effect after a new deploy
   - Trigger a new deploy after adding/changing variables
   - Go to Deploys tab and click "Trigger deploy" > "Deploy site"

### Common Issues

1. **Functions not working**
   - Check environment variables are set in Netlify dashboard
   - Verify function paths in `netlify.toml`
   - Check function logs in Netlify dashboard
   - **Important**: Redeploy after adding environment variables

2. **API key errors**
   - Ensure environment variables are correctly named (case-sensitive)
   - Verify API keys are valid and have sufficient credits
   - Check API key permissions
   - Use the test function to verify variables are loaded

3. **CORS errors**
   - Functions include proper CORS headers
   - Check browser console for specific errors

### Debugging

1. **Check Function Logs**
   - Go to Netlify dashboard > Functions
   - Click on function name to view logs

2. **Test Functions Directly**
   ```bash
   # Test OpenAI function
   curl -X POST https://your-site.netlify.app/.netlify/functions/openai-chat \
     -H "Content-Type: application/json" \
     -d '{"messages":[{"role":"user","content":"Hello"}]}'
   ```

## Cost Considerations

- Netlify Functions: 125,000 requests/month free
- OpenAI API: Pay per token usage
- Anthropic API: Pay per token usage

Monitor your usage in respective dashboards to avoid unexpected charges.
