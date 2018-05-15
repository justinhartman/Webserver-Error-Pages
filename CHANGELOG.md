# Change-Log for Apache Error Pages

Below is a detailed change-log, along with specific tasks completed, for each version released to date for Apache Error Pages.

## Version 2.0.2 (15/05/2018)

- [#enhancement](#enhancement)
  - Renamed the Git repo from `Apache-Error-Pages` to `Webserver-Error-Pages` as there is now support for additional webservers.

## Version 2.0.1 (15/05/2018)

- [#new](#new)
  - Moved `/assets/` and `/webfonts/` to new `/src/static/` folder for better organisation.
  - Cleaned up the `/src/` folder by moving all the Apache HTML templates to `/src/apache/` and the minify script now builds the distribution files out of this new folder.
- [#enhancement](#enhancement)
  - Created proper functions for all the minfy scripts:
    - `src/scripts/minify`
    - `src/scripts/minify_iis`
    - `src/scripts/minify_nginx`
    - `src/scripts/minify_other`
  - Changed `src/scripts/minify` script to now copy everything in the `/src/static/` folder so that it acts like the other scripts when installing the assets and fonts.

## Version 2.0.0 (15/05/2018)

- [#new](#new)
  - Added link to Font Awesome License.
  - New templates:
    - `409.html`
    - `410.html`
    - `412.html`
    - `416.html`
    - `417.html`
    - `418.html`
    - `421.html`
    - `422.html`
    - `423.html`
    - `424.html`
    - `426.html`
    - `428.html`
    - `451.html`
    - `506.html`
    - `507.html`
    - `508.html`
    - `510.html`
    - `511.html`
    - `nginx/444.html`
    - `nginx/494.html`
    - `nginx/495.html`
    - `nginx/496.html`
    - `nginx/497.html`
    - `nginx/499.html`
    - `ms-iis/440.html`
    - `ms-iis/449.html`
    - `ms-iis/451.html`
  - All template files missing have now been created. There are no outstanding error codes to add; the list is now exhaustive.
  - Additional Server Support; now supporting Nginx, IIS and others.
  - Added new minification scripts to minify additional templates for:
    - Nginx: `./scripts/minify_nginx`
    - MS IIS: `./scripts/minify_iis`
    - Other: `./scripts/minify_other`
- [#enhancement](#enhancement)
  - Restructured the `/dist/` folder and cleaned it up so it now only contains sub-folders for the respective webservers.
  - Apache templates files have moved from `/dist/` to `/dist/apache/`.

## Version 1.1.0 (14/05/2018)

- [#new](#new)
  - New templates have been created as follows:
    - 520.html
    - 521.html
    - 533.html
  - Added `v1.0.0` of the `package.json` file which contains the dependencies for executing the `minify` script. You can run `$ npm install` from the project root folder and you _should_ have all the Node modules to run `$ ./scripts/minify`.
  - Added `postcss.config.js` to load the `cssnano` plugin.
- [#enhancement](#enhancement)
  - Optimised the `minify` script to now compress the JavaScript contained in the file along with any CSS inputs.
  - Optimised the CSS minification by using `postcss.config.js` to load the `cssnano` plugin which now reduces all CSS to one line of code.
  - New, minified versions for the CSS and HTML files have been created. The HTML templates are now one line of code as is the same with the CSS templates. File size has been reduced as follows:
    - CSS files: from `61 KB` to `44 KB` (`27.87%` file size reduction).
    - HTML files: from `46.3 KB` to `24.1 KB` (`47.95%` file size reduction).
  - Updated `README.md` to include all available HTTP error codes when modifying `httpd.conf`.
- [#bugfix](#bugfix)
  - Removed the commit of `html-minifier` to the project. This would prevent users from cloning the repo in order to run the minification script.

## Version 1.0.1 (14/05/2018)

- [#new](#new)
  - Added `CHANGELOG.md`, `CODE_OF_CONDUCT.md` and `CONTRIBUTING.md` files.
- [#enhancement](#enhancement)
  - Checked in Visual Studio Code workspace file for users of VS Code.
  - Install instructions now included in `README.md` file.
  - Updated `README.md` file with minifying setup included.
- [#bugfix](#bugfix)
  - Set absolute path to css folder (`/ErrorPages/css/`) to ensure that the resources load when running on a production server.
  - Rebuilt all `/dist/` files with the new changes.

## Version 1.0.0 (13/05/2018)

Grab everything you need from the `/dist/` folder. All other files support the creation of the files in this folder.

- [#new](#new)
  - HTML was minified but JavaScript is still unminified.
  - CSS has been minified although I am unclear what the advantage has been. (?)
- [#enhancement](#enhancement)
  - If you're insterested, there is a script that does the minification from source. This file is contained in [src/scripts/minify][script]. Simply run that file and it will:
    - Delete the `/dist/css/` folder.
    - Delete all the error pages (`rm -f ../dist/*.html`).
    - Recreate the `/dist/css/` folder.
    - Minify the HTML for all files in the `/src/` directory.
    - Minify the CSS for all the files in `/src/css/` directory.
    - Output the HTML and CSS to the `/dist/` folder.

[script]: src/scripts/minify
