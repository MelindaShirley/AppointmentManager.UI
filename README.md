# AppointmentManager.UI
1) I have used vue to create the UI
2) Use the command 'npm run serve' from the place where the projected is downloaded
3) If the calls to API fails, the API URL should be marked as safe to proceed so that vue can consume the API.
4) For Import, there could be issues in connecting to amazon service because of CORS. Then just disable cors from the browser locally with the following steps so the downlad works(for Chrome):

Step 1:
Create a shortcut in desktop

Step 2:
Provide the target as '"C:\Program Files\Google\Chrome\Application\chrome.exe" --disable-web-security --disable-gpu --user-data-dir=~/chromeTemp'

[C:\Program Files\Google\Chrome\Application\chrome.exe] should be replaced with the path of installation of chrome application.
