# bid-calculation

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

Connecting Frontend with Backend

To connect the frontend application with the backend and bypass CORS issues during development, follow these steps:

Open the Start Menu:

Click on the Start button or press the Windows key on your keyboard.
Open the Run Dialog:

Press Windows + R to open the Run dialog.
Execute the Command:

Type the following command in the Run dialog and press Enter:
chrome.exe --user-data-dir="C://Chrome dev session" --disable-web-security
This will open a new instance of Google Chrome with web security disabled, allowing cross-origin requests.
