# Building The Project
- Since we are publishing a new version of the application, we should increment the version number. For APKFileShowcaser we use the [Semantic Versioning](https://semver.org/) convention to update the version number.
    - In summary:
      - Given a version number MAJOR.MINOR.PATCH, increment the:
        - MAJOR version when making major (breaking) changes.
        - MINOR version when adding new features or improvements.
        - PATCH version when making bugfixes or small improvements.


- Edit `package.json`, `tauri.conf.json` and `Cargo.toml` to update the version number
- Replace all instances of `"AppName"` inside `tauri.conf.json` and `main.ts` with the name of the Android app we are building the project for
- Run `npm i`
- Inside the `src-tauri/resources` folder, replace the following placeholder files
  - `QR.svg`: The image file for the QR should have `QR.svg` as the filename.
  - `AppName.apk`: When it comes to the APK file the filename should match the string we used to replace "AppName" inside `tauri.conf.json` and `main.ts`, the extension of the file has to be `.apk`.
- Replace the `app-icon.png` file in the root directory with the Android app icon we are building the project for, make sure the image file meets the following requirements:
  - A PNG file with transparency
  - 1024x1024 px
- Run the command `npm run tauri icon`
- Run `npm run tauri build`
- The executable will be placed in: `src-tauri/target/release/AppName.exe`