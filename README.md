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

### ubuntu cheatsheet
```sh
# list all disks including unmounted
sudo fdisk -l

# mount usb disk
#fat32
sudo mount -t vfat /dev/sdb1 /media/external

# HFs+ (apple)
sudo apt-get install hfsprogs
sudo mount -t hfsplus -o force,rw /dev/sdXY /media/mntpoint
sudo fsck.hfsplus -f /dev/sdXY

# unmount
umount /media/mntpoint

# kernel version
uname -r

# ubuntu version
lsb_release -a

```


### `@reduxjs/toolkit`

<table>
<tr>
<th>
Redux Boilerplate
</th>
<th>
  
```@reduxjs/toolkit```

</th>
</tr>

<tr>

<td>
<pre>

```js

import React, { useReducer } from "react";

const LOGIN_START = "LOGIN_START";
const LOGIN_SUCCESS = "LOGIN_SUCCESS";

function loginStart(payload) {
  return {
    type: LOGIN_START,
    payload
  };
}
function loginSuccess(payload) {
  return {
    type: LOGIN_SUCCESS,
    payload
  };
}

const authState = {
  isRequestingToken: "",
  username: "",
  token: "",
  error: ""
};

function authReducer(state, action) {
  switch (action.type) {
    case LOGIN_START:
      return {
        ...state,
        isRequestingToken: "yes",
        username: action.payload.username
      };
    case LOGIN_SUCCESS:
      return { 
        ...state, 
        isRequestingToken: "no", 
        token: action.payload.token };
    default:
      return state;
  }
}

export function SillyThings() {
  const [state, dispatch] = useReducer(authReducer, authState);

  function handleSubmit(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const username = formData.get("username");

    dispatch(loginStart({ username }));

    // omit for brevity

  }
    
    // omit for brevity

}
```

</pre>
</td>

<td>
<pre>

```js
import React, { useReducer } from "react";
import { createAction, createReducer } from "@reduxjs/toolkit";

const loginStart = createAction("loginStart");
const loginSuccess = createAction("loginSuccess");

const authState = {
  isRequestingToken: "",
  username: "",
  token: "",
  error: ""
};

const authReducer = createReducer(authState, {
  [loginStart]: (state, action) => {
    state.isRequestingToken = "yes";
    state.username = action.payload.username;
  },
  [loginSuccess]: (state, action) => {
    state.isRequestingToken = "no";
    state.token = action.payload.token;
  }
});

export function SillyThings() {
  const [state, dispatch] = useReducer(authReducer, authState);

  function handleSubmit(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const username = formData.get("username");

    dispatch(loginStart({ username }));

    // omit for brevity

  }
    
    // omit for brevity

}
```

</pre>
</td>

</tr>
</table>
