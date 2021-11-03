- 👋 Hi, I’m a full stack developer
- 👀 I’m interested in Software Projects
- 🌱 I’m currently learning Desktop app development using electronjs
- 💞️ I’m looking to collaborate on reactjs, express-node, electron, python projects
- 📫 How to reach me ...
[![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/bukotsunikki.svg?style=social&label=Follow%20%40tonyvx)](https://twitter.com/tony_v007)

### Index
1. [Create a Ubuntu webapp with Icon](#create-a-ubuntu-webapp-with-icon)
2. [ubuntu cheatsheet](#ubuntu-cheatsheet)
3. [JSS Cheat sheet - Pseudo and Nested Selectors](#jss-cheat-sheet---pseudo-and-nested-selectors)
4. [`@reduxjs/toolkit`](#reduxjstoolkit)

<!---
tonyvx/tonyvx is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
### Create a Ubuntu webapp with Icon 
[Back to top](#index)

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
[Back to top](#index)

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

### express node app generator
[Back to top](#index)

_Refer [Express application generator](https://expressjs.com/en/starter/generator.html)_
```sh
npx express-generator
```

### JSS Cheat sheet - Pseudo and Nested Selectors
[Back to top](#index)

### Use `&` to reference selector of the parent rule

```javascript
const styles = {
  container: {
    padding: 20,
    '&:hover': {
      background: 'blue'
    },
    // Add a global .clear class to the container.
    '&.clear': {
      clear: 'both'
    },
    // Reference a global .button scoped to the container.
    '& .button': {
      background: 'red'
    },
    // Use multiple container refs in one selector
    '&.selected, &.active': {
      border: '1px solid red'
    }
  }
}
```

Compiles to:

```css
.container-0 {
  padding: 20px;
}
.container-0:hover {
  background: blue;
}
.container-0.clear {
  clear: both;
}
.container-0 .button {
  background: red;
}
.container-0.selected,
.container-0.active {
  border: 1px solid red;
}
```

### Use `$ruleName` to reference a local rule within the same style sheet

```javascript
const styles = {
  container: {
    // Reference the local rule "button".
    '& $button': {
      padding: '10px'
    },
    // Multiple local refs in one rule.
    '&:hover $button, &:active $button': {
      color: 'red'
    },
    '&:focus $button': {
      color: 'blue'
    }
  },
  button: {
    color: 'grey'
  }
}
```

Compiles to:

```css
.button-1 {
  color: grey;
}
.container-0 .button-1 {
  padding: 10px;
}
.container-0:hover .button-1,
.container-0:active .button-1 {
  color: red;
}
.container-0:focus .button-1 {
  color: blue;
}
```

### Nest at-rules

```javascript
const styles = {
  button: {
    color: 'red',
    '@media (min-width: 1024px)': {
      width: 200
    }
  }
}
```

Compiles to:

```css
.button-0 {
  color: red;
}
@media (min-width: 1024px) {
  .button-0 {
    width: 200px;
  }
}
```

### Deep nesting

```javascript
const styles = {
  button: {
    '&$warn': {
      color: 'red',
      '&:hover, &:focus': {
        color: 'white',
        background: 'red'
      }
    }
  },
  warn: {}
}
```

Compiles to:

```css
.button-0.warn-1 {
  color: red;
}
.button-0.warn-1:hover,
.button-0.warn-1:focus {
  color: white;
  background: red;
}
```

### Increase specificity

When extending third party libraries with high secificity selector it's often necessary to also have a high specificity selector.

```javascript
const styles = {
  button: {
    '.button &': {
      color: 'red'
    }
  }
}
```

Compiles to:

```css
.button .button-0 {
  color: 'red';
}
```

### Demo

[CodeSandbox](//codesandbox.io/s/github/cssinjs/jss/tree/master/examples/plugins/jss-plugin-nested?fontsize=14)


### `@reduxjs/toolkit`
[Back to top](#index)

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
