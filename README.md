# Upload Video Automation App

This app automatically uploads videos saved to a specific folder on your Mac (e.g., Desktop) to YouTube as "Unlisted" videos. It generates appropriate titles and descriptions for the videos, sends a macOS toast notification with the video link, and copies the link to the clipboard.

---

## **Features**
- Monitors the specified folder (`/Users/homesachin/Desktop`) for new video files.
- Automatically uploads new videos to YouTube with unique titles and descriptions.
- Sends a macOS toast notification with the video link.
- Copies the video link to the clipboard.
- Runs automatically at macOS startup using a Launch Agent.
- Keeps running in the background unless manually stopped.

---

## **Requirements**

### **System Requirements**
- macOS
- Python 3.8 or higher

### **Python Libraries**
Install the required Python libraries using the following command:
```bash
pip install watchdog google-auth google-api-python-client google-auth-oauthlib pync pyperclip
```

---

## **Installation and Setup**

### **Step 1: Clone the Repository**
Clone or download the app files to your system:
```bash
git clone https://github.com/sachnaror/upload_video_app.git
cd upload_video_app
```

### **Step 2: Configure YouTube API**
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Enable the **YouTube Data API v3**.
3. Create an OAuth 2.0 client ID.
4. Download the `client_secrets.json` file and place it in the app folder.

### **Step 3: Create a macOS Launch Agent**
1. Create a Launch Agent file to ensure the app runs at startup:
   ```bash
   nano ~/Library/LaunchAgents/com.upload_video.plist
   ```
2. Add the following content to the file:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
       <key>Label</key>
       <string>com.upload_video</string>

       <key>ProgramArguments</key>
       <array>
           <string>/usr/bin/python3</string>
           <string>/Users/homesachin/Desktop/zoneone/practice/shell_scripts/upload_video.py</string>
       </array>

       <key>RunAtLoad</key>
       <true/>

       <key>KeepAlive</key>
       <true/>

       <key>StandardOutPath</key>
       <string>/tmp/upload_video.log</string>

       <key>StandardErrorPath</key>
       <string>/tmp/upload_video_error.log</string>
   </dict>
   </plist>
   ```

3. Load the Launch Agent:
   ```bash
   launchctl load ~/Library/LaunchAgents/com.upload_video.plist
   ```

4. Verify it is running:
   ```bash
   launchctl list | grep com.upload_video
   ```

---

## **Usage**
1. Place a video file (`.mov`, `.mp4`, `.mpeg`) in the folder `/Users/homesachin/Desktop`.
2. The app will automatically:
   - Upload the video to YouTube as "Unlisted."
   - Generate a unique title and description for the video.
   - Notify you with a toast notification containing the YouTube link.
   - Copy the YouTube link to your clipboard.

---

## **Stopping the App**
To stop the app from running automatically:
1. Unload the Launch Agent:
   ```bash
   launchctl unload ~/Library/LaunchAgents/com.upload_video.plist
   ```
2. Manually stop the Python script if running:
   ```bash
   pkill -f upload_video.py
   ```

---

## **Logs**
Logs are saved in the `/tmp` directory:
- Standard output: `/tmp/upload_video.log`
- Errors: `/tmp/upload_video_error.log`

---

## **Troubleshooting**
- **Authentication Issues:**
  Ensure `client_secrets.json` is correctly configured and accessible.
- **Dependencies Not Installed:**
  Run `pip install -r requirements.txt` to install missing libraries.
- **File Not Detected:**
  Ensure the monitored folder is correct (`/Users/homesachin/Desktop`).

---

## **📩 Contact**

| Name              | Details                             |
|-------------------|-------------------------------------|
| **👨‍💻 Developer**  | Sachin Arora                      |
| **📧 Email**       | [sachnaror@gmail.com](mailto:sachnaror@gmail.com) |
| **📍 Location**    | Noida, India                       |
| **📂 GitHub**      | [github.com/sachnaror](https://github.com/sachnaror) |
| **🌐 Website**     | [https://about.me/sachin-arora](https://about.me/sachin-arora) |
| **📱 Phone**       | [+91 9560330483](tel:+919560330483) |

---

## **License**
This project is licensed under the MIT License.
