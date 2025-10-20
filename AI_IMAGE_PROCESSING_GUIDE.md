# AI Agent Image Processing Guide

This guide provides instructions for AI agents to correctly create thumbnail images for the photography portfolio website.

## Overview

The photography portfolio uses a consistent thumbnail format:
- **Size**: 654x654 pixels (square)
- **Format**: JPEG 
- **Naming**: Original filename with `_min` suffix (e.g., `DSCF4199.JPG` → `DSCF4199_min.jpeg`)

## Correct Image Processing Steps

### Step 1: Check Original Dimensions
```bash
sips -g pixelWidth -g pixelHeight images/[IMAGE_NAME]
```

### Step 2: Create Thumbnail (Two-step process)
The key is to **resize first, then crop** to preserve image composition:

```bash
# Step 2a: Resize to manageable size (preserves composition)
sips --resampleHeightWidthMax 1000 images/[IMAGE_NAME] --out images/[IMAGE_NAME]_resized_temp.jpg

# Step 2b: Crop to square thumbnail
sips --cropToHeightWidth 654 654 images/[IMAGE_NAME]_resized_temp.jpg --out images/[IMAGE_NAME_WITHOUT_EXTENSION]_min.jpeg

# Step 2c: Clean up temporary file
rm images/[IMAGE_NAME]_resized_temp.jpg
```

### One-line Command (Recommended)
```bash
sips --resampleHeightWidthMax 1000 images/[IMAGE_NAME] --out images/[IMAGE_NAME]_resized_temp.jpg && sips --cropToHeightWidth 654 654 images/[IMAGE_NAME]_resized_temp.jpg --out images/[IMAGE_NAME_WITHOUT_EXTENSION]_min.jpeg && rm images/[IMAGE_NAME]_resized_temp.jpg
```

## Example Usage

For image `DSCF4199.JPG`:
```bash
sips --resampleHeightWidthMax 1000 images/DSCF4199.JPG --out images/DSCF4199_resized_temp.jpg && sips --cropToHeightWidth 654 654 images/DSCF4199_resized_temp.jpg --out images/DSCF4199_min.jpeg && rm images/DSCF4199_resized_temp.jpg
```

## Why This Method Works

1. **Resize First**: Reduces the original high-resolution image (e.g., 4416x2944) to ~1000px max dimension
2. **Then Crop**: Creates a square crop that shows more of the original image composition
3. **Result**: Thumbnail that maintains the visual essence of the original image

## Common Mistakes to Avoid

❌ **Wrong**: Direct crop without resizing
```bash
sips --cropToHeightWidth 654 654 images/IMAGE_NAME --out images/IMAGE_min.jpeg
```
*This creates thumbnails that are too tightly cropped*

✅ **Correct**: Resize then crop (as shown above)

## File Naming Convention

- Original: `IMAGE_NAME.JPG`
- Thumbnail: `IMAGE_NAME_min.jpeg` (note the lowercase `.jpeg` extension)

## Integration with HTML

After creating the thumbnail, update the HTML in `index.html`:
```html
<div class="col-6 col-sm-6 col-md-4 col-lg-3 col-xl-3 item" data-aos="fade" data-src="images/IMAGE_NAME.JPG" data-sub-html="<h4></h4><p></p>">
  <a href="#">
    <span class="icon-expand"></span>
    <img src="images/IMAGE_NAME_min.jpeg" alt="Image" class="img-fluid">
  </a>
</div>
```

Where:
- `data-src`: Points to full-size image (opens in lightbox)
- `img src`: Points to thumbnail (shows in gallery grid)
