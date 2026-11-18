SHREEJI MARKETING — DEPLOYMENT GUIDE
Repository: https://github.com/krishnapatel04756-jpg/shreeji-marketing-system
Expected website: https://krishnapatel04756-jpg.github.io/shreeji-marketing-system/
Google OAuth JavaScript origin: https://krishnapatel04756-jpg.github.io

WHAT IS HOSTED WHERE
- GitHub Pages hosts only the static website files over HTTPS.
- Google Drive is the only business-data integration and stores the app's business files in the Shreeji Marketing Data folder.
- Do not upload business records, backup files, OAuth tokens, client secrets, invoices, or passwords to this public repository.
- The repository is public, so the website source is visible to anyone.

FILES ALREADY UPLOADED
- index.html — Shreeji Marketing application
- privacy.html — Privacy Notice
- terms.html — Terms of Use
- .nojekyll — disables Jekyll processing
- README_HOSTING.txt — this guide
- TEST_CHECKLIST.txt — pre-production checklist

ONE REMAINING GITHUB ACTION
The files are committed to the main branch. To enable Pages:
1. Open https://github.com/krishnapatel04756-jpg/shreeji-marketing-system/settings/pages
2. Under Build and deployment, set Source to “Deploy from a branch”.
3. Set Branch to “main”.
4. Set Folder to “/(root)”.
5. Click Save.
6. Open the Actions tab and watch the Pages build/deployment. Wait until it succeeds.
7. Then open https://krishnapatel04756-jpg.github.io/shreeji-marketing-system/

The site is not confirmed live until the Pages deployment succeeds and the HTTPS address opens.

GOOGLE OAUTH CONFIGURATION
1. Open https://console.cloud.google.com/auth/clients
2. Select the Google Cloud project used by Shreeji Marketing.
3. Open the OAuth client of type “Web application”.
4. Under Authorized JavaScript origins, add this exact origin:
   https://krishnapatel04756-jpg.github.io
5. Do NOT include /shreeji-marketing-system/ or index.html in the origin.
6. Save.
7. In Google Auth Platform → Audience, add the two intended Google accounts as test users while the consent screen is in Testing.
8. Confirm Google Drive API is enabled.
9. The app requests https://www.googleapis.com/auth/drive. This is a broad Drive scope: Google describes it as view/edit/create/delete access to all files in the authorizing account's Drive. Review the permission before granting it.

TWO-COMPUTER SETUP
Computer 1 (Administrator):
1. Open the HTTPS website.
2. Paste the OAuth Client ID and tick the Drive permission acknowledgement.
3. Click “First computer: create the shared data folder”.
4. Sign in with the Google account that owns the business Drive folder.
5. Complete the app's Administrator/Staff setup.
6. In Google Drive online, share only the “Shreeji Marketing Data” folder with the second intended Google account as Editor.

Computer 2 (Staff):
1. Open the same HTTPS website.
2. Use the same OAuth Client ID and tick the Drive permission acknowledgement.
3. Click “Sign in and connect to existing folder”.
4. Sign in with the second Google account and connect the existing shared folder.
5. Sign in with the Staff app credentials configured on computer 1.
6. Do not create a second data folder or a second set of app accounts.

SECURITY AND OPERATIONAL LIMITATIONS — READ BEFORE LIVE BUSINESS USE
- GitHub Pages is static hosting. It has no private application server and cannot enforce Administrator/Staff permissions on the server.
- Both Google accounts need write access to the shared Drive folder for this direct-to-Drive design. The Editor can also modify/delete Drive files outside the app. Staff deletion restrictions in this version are app-workflow controls only and are not a strong security boundary.
- Google Drive file storage is not a transactional database. The app's write lock is advisory. Do not process stock-changing transactions on both computers at the same time. Finish on one computer, wait for the save to finish, then use Sync Now on the other.
- This is not a fully hardened production accounting system. Do not enter live dealer balances or live inventory until all acceptance checks pass and you are comfortable with the access model.
- OAuth Testing status may require periodic reauthorization. The app holds access tokens in browser memory and does not implement long-lived refresh-token storage.

UPDATING THE WEBSITE
Upload revised website files to this repository and commit them to main. GitHub Pages will rebuild the site from the repository root.
