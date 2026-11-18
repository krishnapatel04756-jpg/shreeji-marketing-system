SHREEJI MARKETING — PERMANENT HTTPS WEBSITE SETUP

Recommended host: GitHub Pages (static website hosting)
Business data store: Google Drive only

WHAT THIS DOES
- Publishes the browser application at a stable HTTPS address.
- GitHub Pages only serves the HTML website. It is NOT connected to the app's business data.
- The application continues to store its business files in the “Shreeji Marketing Data” folder in online Google Drive.
- No Google Drive for desktop, Supabase, Firebase, Google Sheets, or other business-data integration is used.

BEFORE YOU START
- You need a GitHub account. GitHub Pages is available on GitHub Free for public repositories.
- The site source code will be publicly visible in the repository. The package contains no business data, OAuth client secret, Drive access token, or live account passwords. Never upload your Drive data folder, backup files, or credentials to the website repository.
- GitHub Pages sites are publicly reachable. Anyone can load the login/connect screen; Google authorization and the app's own login are separate gates. Do not treat the URL itself as private access control.

PART A — PUBLISH THE WEBSITE
1. Open https://github.com and sign in or create a GitHub account.
2. Click the + menu, then New repository.
3. Repository name: shreeji-marketing-system
4. Choose Public (GitHub Free supports Pages for public repositories).
5. Click Create repository. You do not need to add a README or license.
6. In the new repository, choose Add file → Upload files.
7. From this deployment package, upload these four items to the top/root of the repository:
   - index.html
   - privacy.html
   - terms.html
   - .nojekyll
   Do not upload any files from your Google Drive business folder.
8. Click Commit changes.
9. Open the repository Settings → Pages.
10. Under Build and deployment, choose “Deploy from a branch”.
11. Select Branch: main and Folder: /(root), then Save.
12. Wait for GitHub Pages to finish publishing. The address will be:
    https://YOUR-GITHUB-USERNAME.github.io/shreeji-marketing-system/
13. Open that HTTPS address. The page should show the Shreeji Marketing Drive connection screen.

PART B — CONFIGURE GOOGLE OAUTH FOR THE HOSTED WEBSITE
1. Open https://console.cloud.google.com/auth/clients and select your existing Shreeji Marketing Drive project.
2. Open the Web application OAuth Client ID used by Shreeji Marketing.
3. Under Authorized JavaScript origins, add the website origin only:
    https://YOUR-GITHUB-USERNAME.github.io
   IMPORTANT: Do NOT include /shreeji-marketing-system/ or index.html. An origin is only scheme + hostname + optional port.
4. Keep any existing localhost origin only if you still want local testing. Save.
5. In Google Auth Platform → Audience, keep External / Testing for a private two-person setup, and list both intended Google accounts as Test users. If both accounts belong to the same Google Workspace organization, an Internal app may be appropriate instead.
6. Confirm Google Drive API is enabled and the Drive scope used by this app is listed under Data Access:
    https://www.googleapis.com/auth/drive
7. Reload the published HTTPS site and try Google authorization again. Use the same OAuth Client ID on both computers.

PART C — CONNECT THE TWO COMPUTERS
COMPUTER 1 (ADMINISTRATOR)
1. Open the published HTTPS URL.
2. Paste the OAuth Client ID.
3. Tick the Google Drive permission acknowledgement.
4. Click “First computer: create the shared data folder”.
5. Sign in as the Google account that owns the business Drive data and approve the requested permission.
6. Complete the Administrator and Staff setup.
7. In Google Drive online, share the “Shreeji Marketing Data” folder with only the second intended Google account as Editor.

COMPUTER 2 (STAFF)
1. Open the same published HTTPS URL.
2. Paste the same OAuth Client ID.
3. Tick the permission acknowledgement.
4. Click “Sign in and connect to existing folder”.
5. Sign in with the second Google account and connect to the folder shared by Computer 1.
6. Sign in to Shreeji Marketing using the existing Staff account. Do not create a second data folder or a second set of app users.

OAUTH / TESTING NOTES
- The two Google accounts must be added as Test users while the app is in Testing mode.
- Google displays a testing/unverified warning for apps in this state. Only proceed if you recognize your own project and consent to the Drive permission.
- Google's current guidance says external apps in Testing have test-user limits and limited token lifetime. This app uses an access token held in browser memory; it may ask you to authorize again when the token expires. This package does not implement long-lived refresh-token storage.
- The app requests the broad Drive scope (drive). Google describes this as permission to view, edit, create and delete files in the Google Drive account. The app's normal code stores business files in the Shreeji Marketing Data folder, but the permission itself is broader. Review this carefully before authorizing.

IMPORTANT SECURITY / OPERATING LIMITATIONS
- GitHub Pages is static hosting; it does not provide a private application server or server-side role enforcement.
- Both Google accounts need write access to the shared Drive folder for this direct-to-Drive design. A person with Editor access can also alter or delete files directly in Google Drive outside the app. The Staff delete restriction in this version is an application workflow restriction, not a secure Drive-level restriction.
- The current app's write lock is advisory. Google Drive file storage is not an atomic transactional database. Do not make stock-changing transactions on both computers simultaneously. Finish on one computer, wait for save to finish, then Sync Now on the other.
- The site source code is public. Do not put business data, passwords, OAuth client secrets, access tokens, invoices, or backup files in the GitHub repository.
- The OAuth Client ID is not a client secret, but it should only be used with the intended app origins. Never publish an OAuth client secret in browser code.
- GitHub Pages provides HTTPS; after publishing, use only the https:// address. GitHub's documentation warns that Pages sites are public and are not intended for sensitive transactions. This app's business records stay in Drive, but review the hosting and browser security model before using it for live financial operations.

TEST BEFORE LIVE USE
Use TEST_CHECKLIST.txt from the prior application package to test a temporary design, stock batches, FIFO sale, payments, returns, damaged stock, backups, and both computers. Do not enter live inventory until the real Google authorization and two-computer synchronization tests pass.

UPDATING THE WEBSITE
When a revised index.html is supplied, upload the new index.html to the same repository and commit it. GitHub Pages republishes the changed static site. Keep privacy.html, terms.html, and .nojekyll in the repository.