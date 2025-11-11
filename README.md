# personalwebsite-sophia

Personal portfolio website for Sophia Cohen-Pelletier.

## Contact Form Setup (EmailJS)

The contact form uses EmailJS to send emails. Follow these steps to set it up:

### 1. Create an EmailJS Account
1. Go to [EmailJS.com](https://www.emailjs.com/) and sign up for a free account
2. The free plan includes 200 emails per month

### 2. Add an Email Service
1. In your EmailJS dashboard, go to **Email Services**
2. Click **Add New Service**
3. Choose your email provider (Gmail, Outlook, etc.)
4. Follow the instructions to connect your email account
5. Copy your **Service ID** (you'll need this later)

### 3. Create an Email Template
1. Go to **Email Templates** in your EmailJS dashboard
2. Click **Create New Template**
3. Use the following template variables:
   - `{{from_name}}` - Sender's name
   - `{{from_email}}` - Sender's email
   - `{{message}}` - Message content
   - `{{to_name}}` - Your name (Sophia Cohen-Pelletier)

4. Example template:
   ```
   Subject: New Contact Form Message from {{from_name}}
   
   You have received a new message from your portfolio website.
   
   From: {{from_name}} ({{from_email}})
   Message:
   {{message}}
   ```

5. Copy your **Template ID** (you'll need this later)

### 4. Get Your Public Key
1. Go to **Account** → **General** in your EmailJS dashboard
2. Copy your **Public Key**

### 5. Update the Website
1. Open `public/index.html`
2. Find the line with `emailjs.init('YOUR_PUBLIC_KEY')` (around line 418)
3. Replace `YOUR_PUBLIC_KEY` with your actual EmailJS Public Key
4. Find the line with `emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', ...)` (around line 443)
5. Replace `YOUR_SERVICE_ID` with your Service ID
6. Replace `YOUR_TEMPLATE_ID` with your Template ID

### Example:
```javascript
emailjs.init('abc123xyz'); // Your Public Key
emailjs.send('service_abc123', 'template_xyz789', formData);
```

That's it! Your contact form should now send emails to your specified email address.

## Planets Database Page Setup (Firebase Firestore)

The planets page (`planets.html`) displays data from your Firestore "planets" collection. Follow these steps to connect it:

### 1. Get Your Firebase Configuration

1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Select your project: **personalwebsite-sophia**
3. Click the gear icon ⚙️ next to "Project Overview"
4. Select **Project Settings**
5. Scroll down to **Your apps** section
6. If you don't have a web app yet:
   - Click **Add app** → Select the **Web** icon (`</>`)
   - Register your app (you can use any nickname)
   - Copy the configuration object
7. If you already have a web app, click on it and copy the configuration

### 2. Update the Planets Page

1. Open `public/planets.html`
2. Find the `firebaseConfig` object (around line 200)
3. Replace the placeholder values with your actual Firebase config:

```javascript
const firebaseConfig = {
  apiKey: "your-actual-api-key",
  authDomain: "personalwebsite-sophia.firebaseapp.com",
  projectId: "personalwebsite-sophia",
  storageBucket: "personalwebsite-sophia.appspot.com",
  messagingSenderId: "your-messaging-sender-id",
  appId: "your-app-id"
};
```

### 3. Ensure Firestore is Enabled

1. In Firebase Console, go to **Firestore Database**
2. Make sure your database is created and the "planets" collection exists
3. Add some test documents to your "planets" collection if needed

### 4. Test the Page

1. Open `planets.html` in your browser (or deploy to Firebase Hosting)
2. The page should automatically load and display all documents from your "planets" collection
3. Each document will be displayed as a card showing all its fields

### Notes

- The page automatically displays all fields from each planet document
- Field names are automatically formatted (capitalized, underscores replaced with spaces)
- The page handles empty collections gracefully
- Make sure your Firestore security rules allow read access (check `firestore.rules`)

## Project Template Usage

The `projectTemplate.html` file is a reusable template for creating project detail pages. Here's how to use it:

### Creating a New Project Page

1. **Copy the template file:**
   ```bash
   cp public/projectTemplate.html public/your-project-name.html
   ```

2. **Open the new file** and find the `projectData` object (around line 300)

3. **Fill in your project information:**
   ```javascript
   const projectData = {
     name: "Your Project Name",
     tagline: "Brief description or tagline",
     pageTitle: "Your Project Name - Sophia Cohen-Pelletier",
     
     // Images (array - can have multiple or leave empty [])
     images: [
       {
         src: "path/to/your/image.jpg",
         alt: "Image description"
       }
     ],
     
     // About paragraphs (array - add multiple paragraphs)
     aboutParagraphs: [
       "First paragraph about your project...",
       "Second paragraph with more details..."
     ],
     
     // Features (can be a list or paragraphs)
     useFeatureList: true, // true for bullet list, false for paragraphs
     features: [
       "Feature 1",
       "Feature 2",
       "Feature 3"
     ],
     
     // Links (array - can have multiple or leave empty [])
     links: [
       {
         text: "View Demo",
         url: "https://example.com",
         newTab: true // opens in new tab
       }
     ],
     
     // Technologies/Softwares
     technologiesTitle: "Softwares Used:",
     technologies: [
       "Unity",
       "Procreate",
       "Other Software"
     ],
     
     // Project details
     details: {
       status: "Completed",
       year: "2025",
       role: "Your Role",
       team: "Team Name"
     }
   };
   ```

4. **Save the file** with your project name

5. **Link from your portfolio:**
   - In `index.html`, find your project card in the projects section
   - Wrap the project card in a link: `<a href="your-project-name.html" class="project-card-link">...</a>`

### Template Features

- **Multiple Images**: Add as many images as you want in the `images` array
- **Multiple Paragraphs**: Add multiple description paragraphs in `aboutParagraphs`
- **Flexible Features**: Use either a bulleted list (`useFeatureList: true`) or paragraphs
- **Multiple Links**: Add demo links, GitHub links, or any other links
- **Customizable**: All text, titles, and content can be customized in the `projectData` object

### Example Usage

See `rab-bit.html` for a real example of how to use this template.
