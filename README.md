# Apache, Nginx and IIS Webserver HTTP Error Pages Replacement

The Apache, Nginx and IIS Error Pages project is a drop-in replacement of beautifully designed, user-friendly Apache 2, Nginx and IIS error pages. If you're tired of having _boring_ error pages displayed to users then these might just be the solution for you.

As of Version 2.0.0 there is now additional support for Nginx, Microsoft IIS and other webservers. Installation instructions are similar to Apache 2 and more details are contained below.

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [Features](#features)
* [Preview](#preview)
	* [Error Page Example](#error-page-example)
	* [Responsive Design](#responsive-design)
		* [Desktop](#desktop)
		* [Tablet](#tablet)
		* [Mobile](#mobile)
* [Installation](#installation)
	* [Copying the Error Pages](#copying-the-error-pages)
	* [Additional Server Support](#additional-server-support)
	* [Modifying your Apache Config file](#modifying-your-apache-config-file)
* [Minification Setup](#minification-setup)
	* [Dependencies](#dependencies)
		* [Installing html-minifier](#installing-html-minifier)
		* [Using Node to install the packages](#using-node-to-install-the-packages)
	* [Running the minify script](#running-the-minify-script)
		* [Additional scripts](#additional-scripts)
			* [Nginx](#nginx)
			* [Microsoft IIS](#microsoft-iis)
			* [Other](#other)
* [Contributing](#contributing)
* [Code of Conduct](#code-of-conduct)
* [Versioning](#versioning)
* [Change-Log](#change-log)
* [Authors](#authors)
* [License](#license)
* [Acknowledgements](#acknowledgements)

<!-- /code_chunk_output -->

## Features

* **Complete off-line functionality**. There is no dependence on an Internet connection for these pages to work. Everything is self-contained in the distribution (`/dist/`) folder.
* A compressed distribution **file size which totals only `78 KB`** (from `111 KB`) and includes Images, CSS, HTML and JavaScript. Total package size is `2.1 MB` with all the _Font Awesome_ and _Web Fonts_ included.
* Fully responsive templates, **works across desktop, tablet and mobile**.
* Animated text, **creating the experience of a terminal console**, outputting the respective error code and description of error on screen.
* Now **full support for Nginx, Microsoft IIS and other webservers** which are non-Apache related.
* There are **54 templates**:
    * **38** are exclusive for Apache.
    * **6** for `Nginx`.
    * **7** general/other HTTP status codes templates.
    * **3** for `Microsoft Internet Information Services`.
* Each template, as well as all CSS files, have been minified to ensure the **smallest possible file size**.
* **Font Awesome icons** used in error messages.

[Installation instructions](#installation) are found below the previews. This shouldn't take you more than **5 minutes** to implement these hand-crafted, custom-designed error pages.

## Preview

### Error Page Example

![404 Error Page][404-template]

### Responsive Design

#### Desktop

![Desktop Version][preview1]

#### Tablet

![Tablet Version][preview2]

#### Mobile

![iOS and Android Version][preview3]

## Installation

Installing the drop-in replacement for Apache 2 error pages comes in two parts. First, you need to copy all the files contained within the `/dist/apache/` folder to a location on your server. Second, you need to edit your `apache.conf` or `httpd.conf` file to link the error pages to your server installation.

### Copying the Error Pages

A typical Apache 2 installation will already have a set of Error pages contained as part of the installation. Your path to the error pages will vary but for this example we will assume that your Apache 2 default `www` folder is installed under `/usr/local/var/www/`. Within this location you will see Apache's default error pages contained at `/usr/local/var/www/error/`.

Do not replace the default error pages with this project's files. Instead, install them in a different, but accessible location that the Apache user can access. These commands will copy the project's error pages to your `www` folder.

```console
$ mkdir -p /usr/local/var/www/error-pages
$ cd Webserver-Error-Pages/
$ cp -R dist/apache/ /usr/local/var/www/error-pages
$ chown -R www:apache /usr/local/var/www/error-pages # see note below.
```

**Note: _Ensure that you replace `www` and `apache`, in the `chown` command above, with your web-server's default user and group._**

Check to see if you have all the required files.

```console
$ ls -lh /usr/local/var/www/error-pages
```

Make sure that you have the following file structure below.

```text
/usr/local/var/www/error-pages
├── 400.html
├── 401.html
├── 403.html
├── 404.html
├── 405.html
├── 406.html
├── 407.html
├── 408.html
├── 409.html
├── 410.html
├── 411.html
├── 412.html
├── 413.html
├── 414.html
├── 415.html
├── 416.html
├── 417.html
├── 418.html
├── 421.html
├── 422.html
├── 423.html
├── 424.html
├── 426.html
├── 428.html
├── 429.html
├── 431.html
├── 451.html
├── 500.html
├── 501.html
├── 502.html
├── 503.html
├── 504.html
├── 505.html
├── 506.html
├── 507.html
├── 508.html
├── 510.html
├── 511.html
├── assets
│   └── imac.svg
├── css
│   ├── breakpoints.css
│   ├── fontawesome-all.css
│   ├── google-fonts.css
│   └── main.css
└── webfonts
    ├── -F63fjptAgt5VM-kVkqdyU8n1i8q131nj-o.woff2
    ├── -F63fjptAgt5VM-kVkqdyU8n1iAq131nj-otFQ.woff2
    ├── -F63fjptAgt5VM-kVkqdyU8n1iEq131nj-otFQ.woff2
    ├── -F63fjptAgt5VM-kVkqdyU8n1iIq131nj-otFQ.woff2
    ├── -F63fjptAgt5VM-kVkqdyU8n1isq131nj-otFQ.woff2
    ├── fa-brands-400.eot
    ├── fa-brands-400.svg
    ├── fa-brands-400.ttf
    ├── fa-brands-400.woff
    ├── fa-brands-400.woff2
    ├── fa-regular-400.eot
    ├── fa-regular-400.svg
    ├── fa-regular-400.ttf
    ├── fa-regular-400.woff
    ├── fa-regular-400.woff2
    ├── fa-solid-900.eot
    ├── fa-solid-900.svg
    ├── fa-solid-900.ttf
    ├── fa-solid-900.woff
    └── fa-solid-900.woff2

3 directories, 63 files
```

### Additional Server Support

In addition to the above Apache error pages there is also support for additional webservers. You can find production-ready, minified template files for the following webservers:

* Nginx files located at `dist/nginx/`
* Microsoft IIS files located at `dist/ms-iis/`
* Other webserver files located at `dist/other/`

You can copy the template files required from any of these additional webserver folders to your server installation.

### Modifying your Apache Config file

Once you have your files in the right location you can now edit either your `apache.conf` or `httpd.conf` file, depending on your particular installation.

You can find the location to your file with the following.

```console
$ locate httpd.conf
/usr/local/etc/httpd/httpd.conf
```

If your system returns nothing, run:

```console
$ locate apache.conf
/usr/local/etc/apache/apache.conf
```

Open the file with your favourite editor.

```console
$ sudo nano /usr/local/etc/httpd/httpd.conf
```

Scroll down until you find the following section in your conf file.

```apache
<IfModule alias_module>
    #
    # Redirect: Allows you to tell clients about documents that used to
    # exist in your server's namespace, but do not anymore. The client
    # will make a new request for the document at its new location.
    # Example:
    # Redirect permanent /foo http://www.example.com/bar
    ...
    ...
</IfModule>
```

Add the following to this section.

```apache
<IfModule alias_module>
    #
    # Redirect: Allows you to tell clients about documents that used to
    # exist in your server's namespace, but do not anymore. The client
    # will make a new request for the document at its new location.
    # Example:
    # Redirect permanent /foo http://www.example.com/bar

    #
    # Error Pages Alias
    #
    Alias /ErrorPages/ /usr/local/var/www/error-pages/
    Alias /ErrorPages/css/ /usr/local/var/www/error-pages/css/
    Alias /ErrorPages/assets/ /usr/local/var/www/error-pages/assets/
</IfModule>
```

Now, scroll down further until you get to this section.

```apache
#
# Customizable error responses come in three flavors:
# 1) plain text 2) local redirects 3) external redirects
#
# Some examples:
#ErrorDocument 500 "The server made a boo boo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 "/cgi-bin/missing_handler.pl"
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
```

Comment out any `ErrorDocument` directives (i.e. it should look like `#ErrorDocument`) and then add your new directives so that your file looks similar to this:

```apache
#
# Customizable error responses come in three flavors:
# 1) plain text 2) local redirects 3) external redirects
#
# Some examples:
#ErrorDocument 500 "The server made a boo boo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 "/cgi-bin/missing_handler.pl"
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
ErrorDocument 400 /ErrorPages/400.html
ErrorDocument 401 /ErrorPages/401.html
ErrorDocument 403 /ErrorPages/403.html
ErrorDocument 404 /ErrorPages/404.html
ErrorDocument 405 /ErrorPages/405.html
ErrorDocument 406 /ErrorPages/406.html
ErrorDocument 407 /ErrorPages/407.html
ErrorDocument 408 /ErrorPages/408.html
ErrorDocument 409 /ErrorPages/409.html
ErrorDocument 410 /ErrorPages/410.html
ErrorDocument 411 /ErrorPages/411.html
ErrorDocument 412 /ErrorPages/412.html
ErrorDocument 413 /ErrorPages/413.html
ErrorDocument 414 /ErrorPages/414.html
ErrorDocument 415 /ErrorPages/415.html
ErrorDocument 416 /ErrorPages/416.html
ErrorDocument 417 /ErrorPages/417.html
# ErrorDocument 418 /ErrorPages/418.html (this isn't working and not sure why)
ErrorDocument 421 /ErrorPages/421.html
ErrorDocument 422 /ErrorPages/422.html
ErrorDocument 423 /ErrorPages/423.html
ErrorDocument 424 /ErrorPages/424.html
ErrorDocument 426 /ErrorPages/426.html
ErrorDocument 428 /ErrorPages/428.html
ErrorDocument 429 /ErrorPages/429.html
ErrorDocument 431 /ErrorPages/431.html
ErrorDocument 451 /ErrorPages/451.html
ErrorDocument 500 /ErrorPages/500.html
ErrorDocument 501 /ErrorPages/501.html
ErrorDocument 502 /ErrorPages/502.html
ErrorDocument 503 /ErrorPages/503.html
ErrorDocument 504 /ErrorPages/504.html
ErrorDocument 505 /ErrorPages/505.html
ErrorDocument 506 /ErrorPages/506.html
ErrorDocument 507 /ErrorPages/507.html
ErrorDocument 508 /ErrorPages/508.html
ErrorDocument 510 /ErrorPages/510.html
ErrorDocument 511 /ErrorPages/511.html
```

Save your file and then test your configuration changes by executing the following.

```console
$ sudo apachectl configtest
```

If you get any message other than `Syntax OK` then you've done something wrong. You will need to check your changes made to the `.conf` file and see where you may have gone wrong.

The final step is to restart Apache so that it loads your new error pages.

```console
$ sudo apachectl restart
```

## Minification Setup

As part of the project I have included both the `/src/` and `/dist/` folders. The difference between the two is that the `/dist/` folder contains minified versions of the `/src/` folder files.

There is a `bash` script, found at [/src/scripts/minify][script] which runs the `html` files through `html-minifier` and the `css` files through `postcss`.

### Dependencies

You will need to install, `html-minifier`, `postcss` (with plugins), and `uglify-js` before you can execute the minifaction script. You can do this by following the commands below.

#### Installing html-minifier

The best way to install `html-minifier` is by running the following commands in the project root folder. _(it is important to note that Node (which provides `npm`) needs to be installed for this to work)_.

```console
$ cd Webserver-Error-Pages/
$ git clone git://github.com/kangax/html-minifier.git
$ cd html-minifier
$ npm link .
```

#### Using Node to install the packages

As of version `v1.1.0` there is now a `package.json` file contained at the root of this project folder. This file contains all the dependencies required to execute the `./src/scripts/minify` script. You can run the following commands and it will install `postcss`, along with various plugins, as well as `uglify-js` which is used by `html-minifier`.

```console
$ npm install
```

You will now have a new `/node_modules/` folder and you should be good to go to execute `./src/scripts/minify`. You can ignore `Installing postcss` and `Installing uglify-js`, in the steps below, as you will have these installed already.

### Running the minify script

You can run the script with this command:

```console
$ cd src/
$ ./scripts/minify
The ../dist/apache folder has been reset.
400.html minified
401.html minified
403.html minified
404.html minified
405.html minified
406.html minified
407.html minified
408.html minified
409.html minified
410.html minified
411.html minified
412.html minified
413.html minified
414.html minified
415.html minified
416.html minified
417.html minified
418.html minified
421.html minified
422.html minified
423.html minified
424.html minified
426.html minified
428.html minified
429.html minified
431.html minified
451.html minified
500.html minified
501.html minified
502.html minified
503.html minified
504.html minified
505.html minified
506.html minified
507.html minified
508.html minified
510.html minified
511.html minified
All the CSS files have now been minified.
Copying the assets and fonts...
Minification Complete!
```

There are no options for running this script. Executing this command will:

* Delete the contents in the `/dist/apache/` folder.
* Recreate the `/dist/apache/css/` folder.
* Minify the HTML for all files in the `/src/apache/` directory.
* Minify the CSS for all the files in `/src/css/` directory.
* Copy unminified assets and fonts in `/src/static/` directory.
* Output the HTML and CSS to the `/dist/apache/` folder.

#### Additional scripts

##### Nginx

There are additional templates which are used only by `nginx`. These templates are included in the `dist/nginx/` folder and the script below will minify the files for this folder.

```console
$ cd src/
$ ./scripts/minify_nginx
The ../dist/nginx folder has been reset.
444.html minified
494.html minified
495.html minified
496.html minified
497.html minified
499.html minified
All the CSS files have now been minified.
Copying the assets and fonts...
Minification Complete!
```

##### Microsoft IIS

There are additional templates which are used only by Microsoft Internet Information Services. These templates are included in the `dist/ms-iis/` folder and the script below will minify the files for this folder.

```console
$ cd src/
$ ./scripts/minify_iis
The ../dist/ms-iis folder has been reset.
440.html minified
449.html minified
451.html minified
All the CSS files have now been minified.
Copying the assets and fonts...
Minification Complete!
```

##### Other

There are additional templates which are used only by other webservers. These templates are included in the `dist/other/` folder and the script below will minify the files for this folder.

```console
$ cd src/
$ ./scripts/minify_other
The ../dist/other folder has been reset.
420.html minified
520.html minified
521.html minified
533.html minified
900.html minified
901.html minified
902.html minified
All the CSS files have now been minified.
Copying the assets and fonts...
Minification Complete!
```

## Contributing

Please read the [CONTRIBUTING.md][CONTRIBUTING] file for details on how you can get involved in the project as well as the process for submitting bugs and pull requests.

## Code of Conduct

Please read the [CODE_OF_CONDUCT.md][COC] file for the guidelines that govern the community.

## Versioning

We use [Semantic Versioning][semver] for software versions of this project. For a list of all the versions available, see the [tags][tags] and [releases][releases] on this repository.

## Change-Log

View the [CHANGELOG.md][changelog] file for a detailed list of changes, along with specific tasks completed for each version released to date.

## Authors

* Justin Hartman - [@justinhartman][author-1]

Also see the list of [contributors][contribs] who have participated in this project.

## License

This work is licensed under the [GNU Affero General Public License][agpl]. You can view the full LICENSE by [reading this][license] file.

```text
Copyright 2018-2020 Justin Hartman <justin@hartman.me> (https://hartman.me)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program. If not, see <https://www.gnu.org/licenses/>.
```

## Acknowledgements

Thanks go out to the following for the inspiration, images, icons and, in some cases, the code to back this project up.

* [Computer SVG][vector] by Kameleon - License [CC BY 3.0][ccby30].
* Icons by [Font Awesome][fontawesome] - Read [License here][fa-license].
* [html-minifier][html-min] - for compressing the `/src/*.html`  files into the `/dist/*.html` folder. License: [MIT][mit].
* [PostCSS][postcss] - for compressing the `/src/css/` css files into the `/dist/css/` folder. License: [MIT][mit].
* [@maicong/ErrorPages][maicong] - for the terminal/console output code. License: [MIT][mit].
* [@trimstray/http-error-pages][trimstray] - for giving me the inspiration to use icons as part of the design. License: [GPLv3][gpl].
* [@jongha/httperrorpages][jongha] - for the error pages status message descriptions. License: [MIT][mit].
* [@justinhartman/.github][.github] - for the awesome Github project templates.

[html-min]: https://github.com/kangax/html-minifier
[postcss]: https://github.com/postcss/postcss
[maicong]: https://github.com/maicong/ErrorPages
[vector]: https://www.brandeps.com/icon/C/Coding-Html-01
[ccby30]: https://creativecommons.org/licenses/by/3.0/
[ccby40]: https://creativecommons.org/licenses/by/4.0/
[jongha]: https://github.com/jongha/httperrorpages
[mit]: https://opensource.org/licenses/MIT
[gpl]: http://www.gnu.org/licenses/#GPL
[trimstray]: https://github.com/trimstray/http-error-pages
[fontawesome]: https://www.fontawesome.com
[fa-license]: licenses/LICENSE.txt
[agpl]: https://opensource.org/licenses/AGPL-3.0
[site]: https://justin.hartman.me
[email]: mailto:justin@hartman.me?subject=Github+Contact
[license]: LICENSE
[404-template]: src/docs/preview.gif
[CONTRIBUTING]: CONTRIBUTING.md
[COC]: CODE_OF_CONDUCT.md
[changelog]: CHANGELOG.md
[semver]: http://semver.org
[tags]: https://github.com/justinhartman/Webserver-Error-Pages/tags
[releases]: https://github.com/justinhartman/Webserver-Error-Pages/releases
[contribs]: https://github.com/justinhartman/Webserver-Error-Pages/contributors
[author-1]: https://github.com/justinhartman
[.github]: https://github.com/justinhartman/.github
[script]: src/scripts/minify
[preview1]: src/docs/desktop.png
[preview2]: src/docs/tablet.png
[preview3]: src/docs/mobile.png
