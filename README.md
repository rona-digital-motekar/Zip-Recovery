# ZIP Recovery Lab v2

Static browser app for clue-based recovery of ZIP archives that the user owns or is authorized to access.

## What's new in v2
- Pins `@zip.js/zip.js` to version `2.24.0` instead of importing an unpinned latest build.
- Keeps one `ZipReader` open during the candidate run rather than reopening and reparsing the archive for every candidate.
- Shows the archive file list, which entries are encrypted, and the encryption family when the archive metadata exposes it (ZipCrypto / WinZip AES).
- Allows checking the first encrypted entry or all encrypted entries. The default is all encrypted entries.
- Verifies decrypted content with CRC-32 where applicable and AES authentication-code validation.
- Handles the common `ERR_INVALID_PASSWORD`, `ERR_INVALID_AUTHENTICATION_CODE`, and ZipCrypto CRC/decompression false-positive cases as candidate mismatches; unexpected archive/codec errors are reported separately.
- Candidate builder supports case variants, alternating case, pairwise clue-word combinations, prefix/suffix numbers, optional number insertion, reverse text, common punctuation, and manual candidates.
- Adds candidate export, speed/progress stats, and a clearer result state.

## Deploy on GitHub Pages
1. Extract this project ZIP.
2. Upload `index.html` to the root of your existing GitHub Pages repository, replacing the old file.
3. Commit the change and wait for the Pages deployment to finish.
4. Hard-refresh the site or clear its cached page if the old version remains visible.

## Use
1. Open the GitHub Pages URL while connected to the internet (the ZIP library is loaded from esm.sh).
2. Select your ZIP archive.
3. Read the encrypted-entry list and add words/numbers from the assignment clues.
4. Select targeted pattern rules and build the candidate list.
5. Run recovery. The default mode checks every encrypted entry against the same candidate.
6. A successful result is only shown after the selected encrypted file contents pass the library's decryption/integrity checks.

## Privacy and limitations
- ZIP contents, images, and candidate lists are processed in the browser; they are not uploaded by this app.
- The external CDN is used only to load the `zip.js` library. An internet connection is required for the first load.
- There is no OCR. The user must read the clue image and enter its text manually.
- Candidate generation is targeted and capped at 10,000 candidates. It is not exhaustive brute force and cannot guarantee recovery if the clues do not contain enough information.
- A corrupted ZIP entry can be indistinguishable from a bad candidate in some ZipCrypto cases. Treat repeated integrity errors as a possible archive-damage issue too.
- Use only for archives you own or are authorized to access.
