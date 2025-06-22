# Gmail Setup Instructions for Vercel Contact Form

## 📧 Email Configuration Steps

### 1. Enable Gmail App Passwords

1. **Go to your Google Account settings**: https://myaccount.google.com/
2. **Navigate to Security** (left sidebar)
3. **Enable 2-Step Verification** (if not already enabled)
4. **Generate App Password**:
   - Go to "2-Step Verification"
   - Scroll down to "App passwords"
   - Click "App passwords"
   - Select "Mail" and "Other (Custom name)"
   - Enter: "Portfolio Website"
   - Copy the generated 16-character password

### 2. Add Environment Variables in Vercel

1. **Go to your Vercel Dashboard**: https://vercel.com/dashboard
2. **Click on your portfolio project**
3. **Go to Settings > Environment Variables**
4. **Add these variables**:

   ```
   GMAIL_USER = sirlaudato@gmail.com
   GMAIL_APP_PASSWORD = [your-16-character-app-password]
   ```

   **Important**: Use the App Password, NOT your regular Gmail password!

### 3. Redeploy Your Site

After adding the environment variables:
1. **Go to Deployments tab**
2. **Click "Redeploy" on your latest deployment**
3. **Or push new changes to trigger auto-deployment**

## 🔧 How It Works

- Visitors fill out your contact form
- Form data is sent to `/api/contact` serverless function
- Function uses nodemailer + Gmail SMTP to send emails
- You receive emails at: **sirlaudato@gmail.com**
- Emails include sender's details and message
- Reply-to is set to the sender's email for easy responses

## 🚨 Security Features

- ✅ Server-side email validation
- ✅ Required field validation
- ✅ CORS protection
- ✅ Environment variables for credentials
- ✅ Error handling and logging

## 📱 Testing

Once deployed with environment variables:
1. Visit your portfolio contact form
2. Fill out and submit a test message
3. Check sirlaudato@gmail.com for the email
4. Verify reply-to works by replying to the test email

## 🔍 Troubleshooting

If emails aren't working:
1. Check Vercel Function logs (Dashboard > Functions tab)
2. Verify environment variables are set correctly
3. Ensure Gmail App Password is correct (not regular password)
4. Check spam folder in Gmail

## 📝 Email Format

You'll receive formatted emails with:
- Sender's name and email
- Subject line prefixed with "Portfolio Contact:"
- Clean HTML formatting
- Plain text fallback
- Easy reply functionality
