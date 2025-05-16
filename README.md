# Trifusion Cryptographic System

![Trifusion Banner](header.png)

The **Trifusion Cryptographic System** is a secure, browser-based application for encrypting and decrypting files using a novel double-layer encryption algorithm combining Armstrong numbers and RGB color transformations. Built as a single HTML file with JavaScript, it operates entirely client-side, ensuring data privacy and offline usability. The system supports multi-file encryption, biometric key generation, and robust user authentication, with a responsive UI featuring real-time file previews and dark mode.

## Features

- **Double-Layer Encryption**: Combines Armstrong number-based XOR operations and RGB color transformations for unique file encryption.
- **Multi-File Support**: Encrypts/decrypts multiple files with compression using `pako` for efficiency.
- **Biometric Key Generation**: Supports password-only, biometric-only (image-based), and hybrid key methods, with preprocessing for fingerprint images.
- **Secure Authentication**: Uses PBKDF2 for password hashing and AES-GCM for credential encryption, stored in `localStorage`.
- **Recovery Key**: Generates a downloadable recovery key during registration for account recovery (not used for login).
- **Performance**: Leverages Web Workers for parallel encryption/decryption and Streams API for chunked file processing.
- **UI/UX**: Includes real-time file previews (images, audio, video, text), progress bars, integrity verification modal, and dark mode toggle.
- **Integrity Checks**: Verifies decrypted files using SHA-256 hashes, with a success modal for valid files.
- **Offline Operation**: No server dependencies, ensuring data stays local.

## Prerequisites

- Modern web browser (e.g., Chrome, Firefox, Edge) with JavaScript enabled.
- Internet connection for initial CDN loading (Tailwind CSS, zxcvbn, pako). For offline use, host dependencies locally.
- No server or backend required.

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/trifusion-cryptographic-system.git
   cd trifusion-cryptographic-system


Serve the Application:

Option 1: Open index.html directly in a browser (may require CORS workaround for local files).
Option 2: Use a local server for proper file handling:npm install -g http-server
http-server .

Access at http://localhost:8080.


Optional: Offline Dependencies:

Download CDN files (tailwind.min.js, zxcvbn.js, pako.min.js) and update <script> tags in index.html to point to local paths.
Example:<script src="./libs/tailwind.min.js"></script>





Usage

Open the Application:

Navigate to index.html in your browser.


Register:

Enter a username and password.
Click Register to create an account. A recovery key (<username>_recovery_key.txt) is downloaded automatically.
Note: Store the recovery key securely (not used for login in this version).


Login:

Enter your username and password.
Click Login to access the cryptographic interface.
Incorrect credentials display an error (e.g., "Login failed: Incorrect password").


Encrypt Files:

Select one or more files using the Source Files input (supports images, audio, video, text, etc.).
Choose a Key Generation Method:
Password Only: Enter a password.
Biometric Only: Upload an image (e.g., fingerprint).
Hybrid: Provide both password and image.


Click Encrypt to process files. Encrypted files are downloaded as enc_<filename>.trifusion.
Monitor progress via the progress bar and status log.


Decrypt Files:

Select .trifusion files.
Provide the same key (password/biometric) used for encryption.
Click Decrypt to download decrypted files (dec_<original_extension>).
A success modal appears if integrity checks pass (SHA-256 hash verification).


Additional Features:

File Preview: View the first selected file (image, audio, video, or text snippet).
Dark Mode: Toggle between light and dark themes.
Logout: Clears session and resets inputs.



Testing
Manual Testing

Register: Use username "alice", password "amrita". Verify recovery key download.
Login: Test with correct ("alice", "amrita") and incorrect ("alice", "wrong") credentials.
Encrypt: Upload multiple files (e.g., text, image), use password method, verify .trifusion outputs.
Decrypt: Decrypt with correct/incorrect keys, check integrity modal and warning for invalid files.
UI: Test file preview, dark mode toggle, and progress bar.

Automated Testing

Set up Cypress for end-to-end testing:npm init -y
npm install cypress --save-dev
npx cypress open


Create a test file (cypress/e2e/trifusion.spec.js) with scenarios for registration, login, encryption, and UI interactions.
Run tests:npx cypress run --spec "cypress/e2e/trifusion.spec.js"



Security Considerations

Encryption Algorithm: The Armstrong + RGB algorithm is custom and non-standard. For production, consider replacing with AES-GCM or ChaCha20.
Credential Storage: Credentials are encrypted with AES-GCM and stored in localStorage, which is vulnerable to XSS attacks. Use secure cookies or a backend for production.
Biometric Preprocessing: Image-based key generation (grayscale hashing) is experimental. Ensure consistent image inputs for reliable key derivation.
Recovery Key: Generated during registration but not used for login. Store securely, as it can decrypt credentials if reintroduced.
CDN Risks: External CDNs may introduce vulnerabilities. Host dependencies locally for critical applications.



Fork the repository.
Create a feature branch (git checkout -b feature/YourFeature).
Commit changes (git commit -m "Add YourFeature").
Push to the branch (git push origin feature/YourFeature).
Open a Pull Request with a detailed description.

Suggested Enhancements

Add a backend for server-side storage and two-way SSL authentication.
Implement two-factor authentication (e.g., OTP via email).
Replace custom encryption with standard algorithms (e.g., AES-256).
Add a dedicated recovery key login page.
Enhance biometric support with WebAuthn.

