- 👋 Hi, I’m a full stack developer
- 👀 I’m interested in Software Projects
- 🌱 I’m currently learning Desktop app development using electronjs
- 💞️ I’m looking to collaborate on reactjs, express-node, electron, python projects
- 📫 How to reach me ...

<!---
tonyvx/tonyvx is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
### Create a Ubuntu webapp with Icon 

* 👨‍💻 Type terminal sudo -H gedit /usr/share/applications/whatsapp-webapp.desktop
* 📋 Copy following text to opened screen
```sh
#!/usr/bin/env xdg-open
[Desktop Entry]
Name=WhatsApp
GenericName=WhatsApp
Comment=WhatsApp desktop webapp
Exec=/opt/google/chrome/google-chrome --app=https://web.whatsapp.com/
Terminal=false
Type=Application
StartupNotify=true
MimeType=text/plain;
# make sure this is full path
Icon=  
Categories=Network;Application;
Keywords=WhatsApp;webapp;
X-Ubuntu-Gettext-Domain=WhatsApp
StartupWMClass=web.whatsapp.com
```
