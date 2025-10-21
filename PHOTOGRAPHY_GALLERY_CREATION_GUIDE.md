# Photography Gallery Page Creation Guide for AI Agents

This guide provides step-by-step instructions for AI agents to create photography gallery pages following the established pattern in this project.

## Project Structure Overview

The photography website follows this structure:
- **Main page** (`index.html`) - Contains mixed gallery of all photos
- **Specialized collection pages** - Dedicated pages for specific photo collections
- **Images organized by collection** - Each collection has its own folder under `images/`

## Step-by-Step Process for Creating New Gallery Pages

### 1. Check Available Images
First, verify what images are available for the new collection:
```bash
ls images/[collection_folder_name]/
```

### 2. Process Images for Web Display

**Image Processing Requirements:**
- Create minimized versions for gallery thumbnails (654x654px)
- Keep thumbnails in the same folder as original images
- Use the established two-step process:
  1. Resize to max 1000px first 
  2. Then crop to 654x654px square

**Commands to use:**
```bash
for img in [IMAGE_NAMES]; do 
  sips --resampleHeightWidthMax 1000 images/[collection_folder]/${img}.JPG --out images/[collection_folder]/${img}_resized_temp.jpg && 
  sips --cropToHeightWidth 654 654 images/[collection_folder]/${img}_resized_temp.jpg --out images/[collection_folder]/${img}_min.jpeg && 
  rm images/[collection_folder]/${img}_resized_temp.jpg; 
done
```

### 3. Create HTML Page

**File naming convention:** Use kebab-case (e.g., `venice-beach-sunset.html`)

**Required HTML Structure:**

#### Head Section
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <link rel="shortcut icon" href="favicon.ico">

  <meta name="description" content="[Collection Name] photography collection by Alex Kushnarenko" />
  <meta name="keywords" content="[relevant keywords for collection]" />

  <!-- Font and CSS includes (copy from existing pages) -->
  
  <!-- Custom top navigation styles (copy from existing pages) -->
  <style>
    /* Include all the existing navigation and gallery styles */
  </style>

  <title>[Collection Name] - Alex Kush Photography</title>
</head>
```

#### Body Structure
```html
<body>
  <div class="site-wrap">
    <!-- Header section with Alex Kush title and Instagram -->
    <header class="site-navbar py-3" role="banner">
      <!-- Copy header structure from existing pages -->
    </header>

    <!-- Top Navigation Menu -->
    <div class="container">
      <nav class="top-nav">
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="griffith-park-views.html">Griffith Park Views</a></li>
          <li><a href="venice-beach-sunset.html">Venice Beach Sunset</a></li>
          <li class="active"><a href="[new-page].html">[New Collection Name]</a></li>
        </ul>
      </nav>
    </div>

    <!-- Page Title and Back Button -->
    <div class="container py-5" data-aos="fade">
      <div class="row">
        <div class="col-lg-8 mx-auto text-center">
          <h1 class="text-white intro">[Collection Name]</h1>
          <p><a href="index.html" class="back-button">← Back to Main Gallery</a></p>
        </div>
      </div>
    </div>

    <!-- Gallery Section -->
    <div class="site-section pt-0 pb-0" data-aos="fade">
      <div class="container-fluid">
        <div class="row" id="lightgallery-[unique-id]">
          <!-- Image items go here -->
        </div>
      </div>
    </div>

  </div>

  <!-- Scripts section (copy from existing pages) -->
  <!-- Important: Update the lightGallery initialization -->
  <script>
    $(document).ready(function(){
      $('#lightgallery-[unique-id]').lightGallery();
    });
  </script>

</body>
</html>
```

#### Gallery Image Structure
For each image in the collection:
```html
<div class="col-6 col-sm-6 col-md-4 col-lg-3 col-xl-3 item" data-aos="fade" data-src="images/[collection_folder]/[IMAGE_NAME].JPG">
  <a href="#">
    <span class="icon-expand"></span>
    <img src="images/[collection_folder]/[IMAGE_NAME]_min.jpeg" alt="Image" class="img-fluid">
  </a>
</div>
```

**Important Notes:**
- `data-src` points to full-size original image
- `src` points to minimized thumbnail version  
- Both files are in the same folder
- No captions or descriptions (as per project requirements)

### 4. Update Navigation on All Pages

Update the navigation menu on ALL existing pages to include the new collection:

**Pages to update:**
- `index.html`
- `griffith-park-views.html` 
- `venice-beach-sunset.html`
- Any other existing collection pages

**Navigation structure:**
```html
<div class="container">
  <nav class="top-nav">
    <ul>
      <li class="active"><a href="index.html">Home</a></li>
      <li><a href="griffith-park-views.html">Griffith Park Views</a></li>
      <li><a href="venice-beach-sunset.html">Venice Beach Sunset</a></li>
      <li><a href="[new-page].html">[New Collection Name]</a></li>
    </ul>
  </nav>
</div>
```

**Set the correct active state:**
- Only the current page should have `class="active"`
- Remove active class from other navigation items

### 5. Important Technical Details

**CSS Requirements:**
- Include all existing custom styles for navigation
- Include gallery item hover effects
- Include expand icon positioning
- Include back button styling

**JavaScript Requirements:**
- Include all existing script imports
- Create unique lightGallery ID for each collection
- Initialize lightGallery with the correct selector

**Image Paths:**
- Always use relative paths from project root
- Keep thumbnails with their originals in collection folders
- Follow naming convention: `[ORIGINAL_NAME]_min.jpeg`

### 6. Quality Checklist

Before considering the page complete:

✅ **Images processed correctly (654x654px thumbnails)**  
✅ **All navigation menus updated across all pages**  
✅ **Active navigation state set correctly**  
✅ **Unique lightGallery ID used**  
✅ **Back button styled and functional**  
✅ **All images display properly in gallery**  
✅ **Lightbox functionality works**  
✅ **No captions or descriptions added**  
✅ **Responsive design maintained**  
✅ **SEO meta tags updated appropriately**

## Common Mistakes to Avoid

❌ **Don't** add image captions or descriptions  
❌ **Don't** forget to update navigation on ALL pages  
❌ **Don't** use generic lightGallery IDs (causes conflicts)  
❌ **Don't** put thumbnails in main images folder  
❌ **Don't** skip the two-step image processing  
❌ **Don't** forget to set active navigation state  
❌ **Don't** copy lightGallery ID from other pages  

## File Organization Example

```
images/
├── griffit_park_views/
│   ├── DSCF7079.JPG (original)
│   ├── DSCF7079_min.jpeg (thumbnail)
│   └── [other images...]
├── venice_beach_sunset/
│   ├── DSCF7777.JPG (original)
│   ├── DSCF7777_min.jpeg (thumbnail)
│   └── [other images...]
└── [new_collection]/
    ├── [IMAGE].JPG (original)
    ├── [IMAGE]_min.jpeg (thumbnail)
    └── [other images...]
```

This structure ensures clean organization and makes maintenance easier.
