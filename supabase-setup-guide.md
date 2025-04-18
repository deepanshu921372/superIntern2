# Step-by-Step Guide for Setting Up Supabase and Fixing Connection Issues

This guide will help you set up a new Supabase project and connect it to your Next.js application.

## 1. Create a New Supabase Project

1. Go to [Supabase Dashboard](https://app.supabase.com)
2. Click "New Project"
3. Enter a name for your project (e.g., "TopInterns")
4. Choose a database password (save this somewhere secure)
5. Select a region closest to your users
6. Click "Create new project"
7. Wait for your project to be created (this may take a few minutes)

## 2. Get Your Supabase Credentials

1. Once your project is created, go to the project dashboard
2. In the left sidebar, click on "Project Settings"
3. Click on "API" in the settings menu
4. You'll find two important values:
   - **Project URL**: This is your `NEXT_PUBLIC_SUPABASE_URL`
   - **anon/public** key: This is your `NEXT_PUBLIC_SUPABASE_ANON_KEY`

## 3. Update Your Environment Variables

1. Open your `.env.local` file in your project root
2. Update the following variables with your new credentials:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-id.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
   ```
3. Save the file

## 4. Run the SQL Setup Script

1. Go back to your Supabase dashboard
2. Click on "SQL Editor" in the left sidebar
3. Click "New Query"
4. Copy and paste the entire contents of the `supabase-setup.sql` file from your project
5. Click "Run" to execute the SQL script
6. Verify that the script ran successfully (no error messages)

## 5. Verify Table Creation

1. In the Supabase dashboard, click on "Table Editor" in the left sidebar
2. You should see an `intern_profiles` table listed
3. Click on the table to verify its structure matches what's defined in the SQL script

## 6. Test Storage Bucket

1. In the Supabase dashboard, click on "Storage" in the left sidebar
2. You should see a `resumes` bucket
3. If not, the application will attempt to create it automatically, but you can also create it manually:
   - Click "New Bucket"
   - Enter "resumes" as the name
   - Enable "Public bucket" option
   - Click "Create bucket"

## 7. Restart Your Application

1. Stop your Next.js development server (if running)
2. Start it again with:
   ```
   npm run dev
   ```

## 8. Debugging Connection Issues

If you're still experiencing connection issues:

1. **Check Browser Console**: Open your browser's developer tools and check the console for error messages
2. **Verify Environment Variables**: Make sure your environment variables are correctly loaded
3. **Check Network Requests**: In the browser's Network tab, look for requests to your Supabase URL and check for errors
4. **Verify RLS Policies**: Make sure the Row Level Security policies are correctly set up
5. **Check CORS Settings**: In Supabase Project Settings > API, verify that your application's URL is in the allowed origins

## 9. Common Error Messages and Solutions

### Empty Error Object `{}`
- This usually indicates a connection issue or missing table
- Make sure your Supabase URL and key are correct
- Verify that the `intern_profiles` table exists
- Check if your IP is allowed in Supabase's network restrictions

### "Table does not exist" Error
- Run the SQL setup script to create the necessary tables
- Make sure the script executed successfully

### Storage Access Issues
- Verify that the storage bucket exists
- Check that the RLS policies for storage are correctly set up

## 10. Testing the Connection

You can test your connection by:

1. Going to your profile page in the application
2. Checking the browser console for connection logs
3. Verifying that the profile data loads correctly

If you continue to experience issues, please provide specific error messages from the browser console for further troubleshooting.
