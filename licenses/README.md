# Third-Party Licenses

This folder contains license information for bundled third-party software.

## Included Components

- **OpenSSL**: Apache License 2.0
- **PowerShell**: MIT License (Linux AppImage only)

## Files

- `THIRD-PARTY-NOTICES.txt` - Main attribution file (distributed with app)
- `OPENSSL-LICENSE.txt` - Downloaded during build
- `POWERSHELL-LICENSE.txt` - Downloaded during build (optional)

## Build Process

During build, these files are:
- Windows: Copied to `Build/licenses/`
- Linux: Embedded in AppImage at `/usr/share/licenses/eclypse-security-manager/`

## Compliance

By including these files, ECLYPSE Security Manager complies with:
- Apache License 2.0 (OpenSSL)
- MIT License (PowerShell)

No source code modifications were made to these components.
