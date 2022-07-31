# **Tauri**
- `Tauri bundler` is part of Tauri CLI and let us compile our binary, package assets, and prepare a final bundle with the following single command:
```rust
tauri build
```
- the first time when we run the above command, it takes some time to collect the Rust crates and build everything, but on subsequent runs, it only needs to rebuild our app's code, which is much quicker
- `tauri build` does several other things for you:
1. Build the Frontend
- if we have configured the `tauri.config.json` correctly, the bundler calls the `beforeBuildCommand` during this step, allowing us to build our Frontend
2. Build Rust Binary
- the bundler calls `cargo build` under the hood and compile the Rust project into a single exectubale. This step also inlines your previously generated Frontend files into the executable. The compiled executable is placed in the `src-tauri/target/release` folder
3. Create Packages
- During this step the bundler collects all necessary files for packaging: the binary, resources, sidecars, icons and app manifests. These files will be packaged up according to the package formats your operating system supports. The created artifacts are located in the `src-tauri/target/release/bundle/` folder.
4. Code Sign
- If you have code-signing enabled, either for Windows, macOS, or the Updater, the last step is signing the created artifacts. This step will create `.sig` files in the `src-tauri/target/release/bundle/` for each supported packaging format.
  
# **Packaging Formats**
- it will detect our OS and build a bundle according, currently it supports:
1. Windows: `.exe, .msi, .msi.zip`
2. macOS: `.app, .dmg, .app.tar.gz`
3. Linux: `.deb, .AppImage, .AppImage.tar.gz`