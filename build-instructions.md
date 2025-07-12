# Building GCTU GradeTrack Desktop App

This guide explains how to build the desktop application from your React project.

## Prerequisites

1. **Node.js** (v16 or higher)
2. **npm** or **yarn**
3. **Windows**: No additional requirements
4. **macOS**: Xcode Command Line Tools
5. **Linux**: Standard build tools

## Development

### Run in Development Mode
```bash
# Start both web server and Electron app
npm run electron:dev
```

### Run Electron Only (after web app is built)
```bash
npm run electron
```

## Building for Production

### 1. Build for Current Platform
```bash
npm run electron:dist
```

This will create a `release` folder with:
- **Windows**: `GCTU GradeTrack Desktop Setup.exe`
- **macOS**: `GCTU GradeTrack Desktop.dmg`
- **Linux**: `GCTU GradeTrack Desktop.AppImage`

### 2. Build for Specific Platform
```bash
# Windows (from any platform)
npx electron-builder --win

# macOS (requires macOS)
npx electron-builder --mac

# Linux (from any platform)
npx electron-builder --linux
```

### 3. Build for All Platforms
```bash
npx electron-builder --win --mac --linux
```

## Output Files

After building, you'll find the installer files in the `release` folder:

### Windows
- `GCTU GradeTrack Desktop Setup.exe` - NSIS installer
- `win-unpacked/` - Unpacked application folder

### macOS
- `GCTU GradeTrack Desktop.dmg` - DMG installer
- `mac/` - Application bundle

### Linux
- `GCTU GradeTrack Desktop.AppImage` - Portable application

## Distribution

### Windows Setup.exe Features:
- ✅ Custom installer with GCTU branding
- ✅ Desktop shortcut creation
- ✅ Start menu integration
- ✅ Uninstaller included
- ✅ User can choose installation directory
- ✅ Auto-updater ready (if configured)

### Installation Process:
1. User downloads `GCTU GradeTrack Desktop Setup.exe`
2. Runs the installer
3. Chooses installation directory
4. App installs with shortcuts
5. Ready to use!

## Troubleshooting

### Common Issues:

1. **Build fails on Windows**:
   ```bash
   npm install --global windows-build-tools
   ```

2. **Icon not showing**:
   - Ensure icon file exists at specified path
   - Use .ico format for Windows, .icns for macOS

3. **App won't start**:
   - Check that `dist` folder exists and contains built React app
   - Verify all dependencies are installed

### Debug Mode:
```bash
# Enable debug logging
DEBUG=electron-builder npm run electron:dist
```

## Customization

### Change App Details:
Edit `package.json` build configuration:
- `appId`: Unique application identifier
- `productName`: Display name
- `copyright`: Copyright notice

### Modify Installer:
Edit `electron-builder.yml` for advanced installer options:
- Custom installer images
- License agreement
- Installation scripts
- File associations

## Security Notes

- App is code-signed ready (add certificates for production)
- Context isolation enabled for security
- Node integration disabled in renderer
- All external links open in default browser