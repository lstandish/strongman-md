# Release Notes

---

### Maintenance team

The current members of the Strongman team:

* [@lstandish](https://github.com/lstandish/)

#### Version 1.45 January 22, 2022
- If Internet connection is lost, no longer set Domain search off.

#### Version 1.44 June 21, 2021
- Changed submodule dependency folder structure. Checking out the submodule source code (git submodule init and git submodule update) is now optional.
- Added minified versions of some javascript dependencies. Added gzip compressed versions of javascript files, in case user wants to configure Apache or another web server to serve pre-compressed js files.

#### Version 1.43 June 17, 2021
- Secure notes field is no longer automatically cleared when username is changed. This facillitates copying changing the domain or username of an entry.
- Updated dependencies: jquery, jshashes, aes-js, javascript-biginteger, moment, papaparse.
- Converted dependencies to git submodules for easier maintenance
- Fixed bug: double quote characters in site passwords, when exportetd to CSV files, would cause import from CSV files to break.  Solution: double quotes are no longer generated in computed passwords. Instead of a double quote, the '~' character is generated. Also, double quotes are no longer allowed in custom passwords. WARNING: This fix will cause any computed password which previously contained a double quote to appear with a '~' character instead.

#### Version 1.42 July 5, 2020
- Rolled back from "Compute/Save" to "Save" button.

#### Version 1.41 July 5, 2020
- Fix bug: username with spaces now works.
- Changed "Compute" button label to "Compute/Save", to clarify that the "password profile is saved to the server when online.

#### Version 1.38 January 7, 2020
- Relaxed master password requirement. When "permit not Diceware" setting is made, Strongman will
warn of weak passwords but will permit any password.

#### Version 1.35 December 26, 2019
- Removed auto-clear of clipboard. (Clipboard should not be cleared without user's conscious intent.)

#### Version 1.34 December 25, 2019
- (bugfix) Fixed password copy to clipboard and clipboard clear on IOS.

#### Version 1.32 December 21, 2019
- (bugfix) Allow clipboard copy to work for older browsers.
- Turning on password-on-focus gives respective password field focus (thus visibility)

#### Version 1.31 December 15, 2019
- (bugfix) Copy of password to clipboard now works for hidden password field (eye-closed icon) 

#### Versions 1.26-1.30 December 3, 2019
- Added password import/export from/to Keepass CSV format
- Made headers configurable for CSV import
- Allowed detection and skipping of malformed row in CSV file import
- Increased length limits for domain and username
- Allowed import and store settings actions for uninitialized account

#### Version 1.25 June 26, 2019
- Master password timeout option
- Improved settings user interface

#### Version 1.20 April 26, 2019
- Added hook for new account actions

#### Version 1.19 April 25, 2019
- Emergency fix for broken offline mode.
- fixed account status message for newly created accounts

#### Version 1.17 April 22, 2019
- Fixed offline mode (was non-working)
- Preventing hammering on ajax-json-list when no account loaded
- fixed autocomplete not opening on first click after master password load
- added submit button for master password. This allows immediate warning about new or weak master password.
- rewrote warning messages about weak master password
- fixed master password check to always check for Diceware first even when Diceware requirement is overridden
- reduced weak master password warning messages when using offline
- added light green background to autocomplete (domain) field to indicate that password profiles are loaded from server and ready to use (either via showing the entire list, or via incremental search
- Changed search/show all switch from "no search" to "search" in UI, to prevent wrapping in cell phone view.  Changed cookie name from "matchoff" to "matchon."
- Compacted UI items above domain input field, including setting a fixed width for filter dropdown selection menu
- Incorporated javascript promise/wait into hashpass function to allow proper handling of offline master password hashing.
- remove more commented code(*initial release*)

#### Version 1.10
Added password category support
Code cleanup
Files cleanup
Upgrade moment.js to latest upstream version

#### Version 1.0 (*initial release*)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwMjUzOTI3N119
-->