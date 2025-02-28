Writeup: Fractured Frames (ACECTF)
🔍 Challenge Overview

We received a suspicious image that had hidden information within its structure. The hint suggested that the image wasn’t erased or encoded, but rather manipulated structurally.
🛠️ Solution Approach

    Checking the Image Dimensions
        Using exiftool to inspect the metadata:

        exiftool image.png

        The height value was modified, which hinted at hidden data.

    Fixing the Image Height
        The solution involved changing the height by 1 pixel.
        This can be done using a hex editor:
            Open the file in a hex editor (hexedit or HXD).
            Locate the height value.
            Change 00 to 01 in the appropriate byte.

    Viewing the Fixed Image
        After adjusting the height, the hidden flag became visible at the bottom of the image.

🏆 Final Flag

After modifying the height, the flag appeared:

ACECTF{th1s_sh0uld_b3_en0u6h}