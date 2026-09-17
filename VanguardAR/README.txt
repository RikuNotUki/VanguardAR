VANGUARD AR - SETUP INSTRUCTIONS
==================================

You have almost everything you need. There's ONE manual step left
(compiling your card images into a tracking file), then a hosting
step, then you're testing on your phone.


STEP 1 — Compile your card images into a .mind file
-----------------------------------------------------
This is the one piece I couldn't generate for you directly.

1. Go to: https://hiukim.github.io/mind-ar-js-doc/tools/compile
2. Click "Choose Files" (or drag-and-drop) and upload these 4 images
   from the "cards" folder, IN THIS EXACT ORDER:

     1. BlasterBlade.jpg   (target index 0)
     2. Flogal.jpg         (target index 1)
     3. Barcgal.jpg        (target index 2)
     4. KnightKay.jpg      (target index 3)

   The order matters - it must match the order the index.html file
   expects (targetIndex: 0, 1, 2, 3 in the code).

3. Click "Start". It'll process each image (takes ~10-30 seconds).
4. Click "Download Compiled" - this saves a file called "targets.mind"
5. Move that "targets.mind" file into THIS SAME FOLDER, right next to
   index.html (not inside "models" or "cards" - the root of this folder).


STEP 2 — Host the folder so your phone can access it
-------------------------------------------------------
AR camera access requires HTTPS (or localhost) - you can't just
double-click index.html and open it directly in a phone browser,
it won't get camera permission that way.

EASIEST FREE OPTION - GitHub Pages:
1. Create a free GitHub account if you don't have one (github.com).
2. Create a new repository (public).
3. Upload this entire folder's contents (index.html, targets.mind,
   the "models" folder, the "cards" folder) into that repository.
4. Go to the repository's Settings > Pages > enable GitHub Pages
   (branch: main, folder: / root).
5. Wait a minute, then GitHub gives you a URL like:
   https://yourusername.github.io/your-repo-name/
6. Open that URL on your phone's browser.

ALTERNATIVE - Netlify Drop (even faster, no account needed):
1. Go to https://app.netlify.com/drop
2. Drag this entire folder onto the page.
3. It instantly gives you a live HTTPS link you can open on your phone.
   (This is probably the fastest way to just test right now.)


STEP 3 — Test it
------------------
1. Open the hosted link on your phone.
2. Allow camera access when prompted.
3. Point your camera at any of your 4 physical cards.
4. That character's real 3D model should appear standing on the card.
5. Tap the character on your screen:
     - Blaster Blade: plays his real "Basic_Jump" animation (used as
       the attack trigger) since he has a working rig/animation.
     - Flogal, Barcgal, Knight Kay: since these three don't have
       baked animations, tapping them does a quick Pokemon-style
       "bump forward and back" lunge on the actual 3D model itself
       (not a flat card image) - a simple position shift, no rig
       needed.


NOTES / THINGS TO KNOW
------------------------
- Blaster Blade's model was compressed from 33.8MB down to ~1.2MB
  (resized textures, WebP conversion, Draco mesh compression) so it
  loads fast on mobile data. It should still look sharp.

- The only animation currently in the Blaster Blade GLB is called
  "Basic_Jump" - there's no separate Idle animation baked in, so he
  just stands in his rest pose until you tap him, then Basic_Jump
  plays once and holds on the last frame. If you want a proper
  looping Idle animation later, that needs to be created and
  exported as its own separate Action in Blender, then re-exported.

- Scale/position of Blaster Blade on the card (currently scale
  "0.3 0.3 0.3", position "0 0 0.2") is a rough guess - you'll very
  likely need to tweak these numbers in index.html once you see it
  on your actual card in AR, since I can't preview it myself.

- All 4 characters now use their real compressed 3D models:
    BlasterBlade.glb  33.8 MB -> 1.2 MB
    Flogal.glb        20.3 MB -> 0.6 MB
    Barcgal.glb       27.3 MB -> 0.8 MB
    KnightKay.glb     26.9 MB -> 0.8 MB
  Same process each time: resized textures, WebP conversion, Draco
  mesh compression, duplicate removal. Should still look sharp on
  a phone screen while loading fast.

- The "cards" folder images are ONLY used for compiling targets.mind
  in Step 1 (they're the tracking images) - they are not displayed
  in the AR scene itself anymore, since all 4 characters now show
  their real 3D models instead of a flat card image.

- If you later get real skeletal animations (Idle/Attack) for Flogal,
  Barcgal, or Knight Kay from Blender/Mixamo, send me the updated
  GLB files and I'll switch those three from the "bump" tap behavior
  over to proper animation-mixer clips, same as Blaster Blade.
