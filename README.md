# mac-issue-solution

# MacBook Pro M4 HDMI Fix

External monitor is not detected through the built-in HDMI port.

## Symptoms

- Monitor shows **No Signal**
- HDMI cable and monitor work with other devices
- Only the built-in display appears in macOS
- Restarting may fix it temporarily

## Solution
# Mac M4: Safe Mode-এ Display Preferences Reset

## ১. প্রস্তুতি / Preparation

1. Mac থেকে HDMI ক্যাবল খুলে রাখুন।  
   Disconnect the HDMI cable from your Mac.

2. আপনার কাজ সেভ করুন।  
   Save your work.

3. নির্দেশনাগুলোর স্ক্রিনশট ফোনে রাখুন অথবা কাগজে লিখে রাখুন—Safe Mode-এ Cursor খোলা নাও থাকতে পারে।  
   Keep screenshots of these instructions on your phone or write them down—Cursor may not open in Safe Mode.

## ২. Safe Mode-এ বুট করুন / Boot into Safe Mode
### Apple Silicon / M4

1. **Apple menu → Shut Down** নির্বাচন করুন। সম্পূর্ণ বন্ধ হওয়া পর্যন্ত অপেক্ষা করুন।  
   Choose **Apple menu → Shut Down** and wait until the Mac shuts down completely.

2. Startup options বা ডিস্ক আইকন আসা পর্যন্ত **পাওয়ার বাটন চেপে ধরে রাখুন**।  
   **Press and hold the power button** until startup options appear.

3. আপনার **startup disk** সিলেক্ট করুন।  
   Select your **startup disk**.

4. **Shift** চেপে ধরে **Continue in Safe Mode** ক্লিক করুন।  
   Hold **Shift**, then click **Continue in Safe Mode**.

5. লগইন করুন। “Safe Boot” লেখা দেখে Safe Mode নিশ্চিত করুন।  
   Log in and look for “Safe Boot” to confirm Safe Mode.

## ৩. Terminal-এ কমান্ড চালান / Run the Commands in Terminal

**Applications → Utilities → Terminal** খুলুন। নিচের ব্লক কপি-পেস্ট করুন।  
Open **Applications → Utilities → Terminal** and paste the following block.

> **সতর্কতা:** এই কমান্ডগুলো display preferences মুছে দেয়। `rm -rf ~/.Trash/*` কমান্ডটি Trash-এর ফাইল স্থায়ীভাবে মুছে দেয়; display reset-এর জন্য এই লাইন প্রয়োজন নেই, চাইলে বাদ দিন।  
> **Warning:** These commands delete display preferences. The `rm -rf ~/.Trash/*` command permanently deletes files in Trash; this line is unnecessary for resetting display preferences and can be omitted.

```bash
sudo rm -f /Library/Preferences/com.apple.windowserver.plist \
  /Library/Preferences/com.apple.windowserver.displays.plist

rm -f ~/Library/Preferences/com.apple.windowserver.plist \
  ~/Library/Preferences/ByHost/com.apple.windowserver*.plist

rm -rf ~/.Trash/*

echo "Done. Files remaining (should be empty):"
ls /Library/Preferences/com.apple.windowserver* 2>/dev/null || echo "system: none"
ls ~/Library/Preferences/ByHost/com.apple.windowserver* 2>/dev/null || echo "user: none"
```

> `sudo` পাসওয়ার্ড চাইলে টাইপ করে **Enter** চাপুন। টাইপ করার সময় কোনো ক্যারেক্টার দেখা যাবে না।  
> If `sudo` asks for your password, type it and press **Enter**. No characters will appear while typing.

## ৪. Normal Restart ও HDMI সংযোগ / Restart Normally and Reconnect HDMI

1. **Apple menu → Restart** নির্বাচন করুন। এবার স্বাভাবিকভাবে বুট হবে।  
   Choose **Apple menu → Restart** to boot normally.

2. ডেস্কটপে লগইন সম্পূর্ণ হওয়ার পরে HDMI ক্যাবল লাগান।  
   Reconnect the HDMI cable after logging in completely.

3. **System Settings → Displays** খুলে external monitor শনাক্ত হয়েছে কি না দেখুন।  
   Open **System Settings → Displays** and check whether the external monitor is detected.

4. প্রয়োজন অনুযায়ী **Arrangement** ও **Resolution** আবার সেট করুন।  
   Adjust **Arrangement** and **Resolution** as needed.
