# Convert Images to WebP Format

## Images to Convert

The following images need to be converted from JPG/PNG to WebP format:

### Required Conversions:
1. `public/assets/hero.jpg` → `public/assets/hero.webp`
2. `public/assets/bg-removed.png` → `public/assets/bg-removed.webp`
3. `public/assets/1.jpg` → `public/assets/1.webp`
4. `public/assets/2.jpg` → `public/assets/2.webp`
5. `public/assets/3.jpg` → `public/assets/3.webp`
6. `public/assets/4.jpg` → `public/assets/4.webp`

## Method 1: Using Online Converter (Easiest)

1. Go to https://cloudconvert.com/jpg-to-webp or https://convertio.co/jpg-webp/
2. Upload each image
3. Convert to WebP format
4. Download and save to `public/assets/` folder

## Method 2: Using Command Line (Bulk Conversion)

### Install cwebp (WebP converter)

**Windows:**
```bash
# Download from: https://developers.google.com/speed/webp/download
# Or use Chocolatey:
choco install webp
```

**Mac:**
```bash
brew install webp
```

**Linux:**
```bash
sudo apt-get install webp
```

### Convert Images

Navigate to your assets folder and run:

```bash
cd public/assets

# Convert individual files
cwebp -q 85 hero.jpg -o hero.webp
cwebp -q 85 bg-removed.png -o bg-removed.webp
cwebp -q 85 1.jpg -o 1.webp
cwebp -q 85 2.jpg -o 2.webp
cwebp -q 85 3.jpg -o 3.webp
cwebp -q 85 4.jpg -o 4.webp

# Or convert all at once (Windows PowerShell)
Get-ChildItem -Filter *.jpg | ForEach-Object { cwebp -q 85 $_.FullName -o ($_.BaseName + ".webp") }
Get-ChildItem -Filter *.png | ForEach-Object { cwebp -q 85 $_.FullName -o ($_.BaseName + ".webp") }
```

## Method 3: Using Node.js Script

Create a file `convert-to-webp.js`:

```javascript
const sharp = require('sharp');
const fs = require('fs');
const path = require('path');

const assetsDir = './public/assets';
const files = [
  'hero.jpg',
  'bg-removed.png',
  '1.jpg',
  '2.jpg',
  '3.jpg',
  '4.jpg'
];

async function convertToWebP() {
  for (const file of files) {
    const inputPath = path.join(assetsDir, file);
    const outputPath = path.join(assetsDir, file.replace(/\.(jpg|png)$/, '.webp'));
    
    try {
      await sharp(inputPath)
        .webp({ quality: 85 })
        .toFile(outputPath);
      console.log(`✓ Converted ${file} to WebP`);
    } catch (error) {
      console.error(`✗ Error converting ${file}:`, error.message);
    }
  }
}

convertToWebP();
```

Install sharp and run:
```bash
npm install sharp
node convert-to-webp.js
```

## Benefits of WebP

- **Smaller file sizes**: 25-35% smaller than JPEG/PNG
- **Faster loading**: Improved page speed and performance
- **Better SEO**: Google favors faster-loading pages
- **Quality**: Maintains visual quality at smaller sizes

## After Conversion

1. Verify all WebP images are in `public/assets/`
2. Test the website to ensure images load correctly
3. (Optional) Delete old JPG/PNG files to save space
4. Clear browser cache to see the new images

## Code Changes Already Made

✓ Hero.jsx - Updated to use hero.webp and bg-removed.webp
✓ ProductDetails.jsx - Updated to use 1.webp, 2.webp, 3.webp, 4.webp

All image references in the code have been updated to use .webp extensions.
