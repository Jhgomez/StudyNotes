* Download AOSP files like this:
  1. For a URL like this `https://android.googlesource.com/platform/development/+/android17-release/apps/OBJViewer/assets.tar.gz`
  2. Download like this `curl -L 'https://android.googlesource.com/platform/development/+archive/android17-release/apps/OBJViewer/assets.tar.gz' -o assets.tar.gz`,
     note `+archive` was added
  3. Unpack like this `mkdir -p assets && tar -xzf assets.tar.gz -C assets`
