# Apache Error Pages Replacement

The Apache Error Pages project is a drop-in replacement of beautifully designed, user-friendly Apache 2 error pages. If you're tired of having _boring_ Apache error pages displayed to users then these might just be the solution for you.
## Features

* Fully responsive templates, works across desktop, tablet and mobile phones.
* Animated text, creating the illusion of an error output on a Terminal console.
* There are 24 templates covering all Apache 2 (as well as other webserver) error statuses. Enjoy!
* Each template, as well as corresponding CSS file, has been minified for smallest file usage possible.
* Font Awesome icons used in error messages.

Installation instructions are found below the previews. This shouldn't take you more than 5-10 minutes to implement these crafted, custom-designed Apache error pages.

## Preview

### 404 Error Page

![404 Error Page][404-template]

## Installation

Installing the drop-in replacement for Apache 2 error pages comes in two parts. You will need to copy all the files contained within the `/dist/` folder to a location on your server. Secondly, you will need to edit your `apache.conf` or `httpd.conf` file to link the error pages to your server.

### Copying the Error Pages

A typical Apache 2 installation will already have a set of Error pages contained as part of the installation. Your path to the error pages will vary but for this example we will assume that your Apache 2 default `www` folder is installed under `/usr/local/var/www/`. Within this location you will see Apache's default error pages contained at `/usr/local/var/www/error/`.

Do not replace the default error pages with this project's files. Instead, install them in a different, but accessible location that the Apache user can access. These commands will copy the project's error pages to your `www` folder.

```bash
$ cd Apache-Error-Pages/
$ cp -R dist/ /usr/local/var/www/error-pages
$ chown -R www:apache /usr/local/var/www/error-pages # see note below. 
```

**NB: _Ensure that you replace `www` and `apache`, in the `chown` command above, with your web-server's default user and group._**

Check to see if you have all the required files.

```bash
$ ls -lh /usr/local/var/www/error-pages
```

Make sure that you have the following file structure below.

```terminal
/usr/local/var/www/error-pages
├── 400.html
├── 401.html
├── 403.html
├── 404.html
├── 405.html
├── 406.html
├── 407.html
├── 408.html
├── 411.html
├── 413.html
├── 414.html
├── 415.html
├── 420.html
├── 429.html
├── 431.html
├── 500.html
├── 501.html
├── 502.html
├── 503.html
├── 504.html
├── 505.html
├── 900.html
├── 901.html
├── 902.html
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
```

### Modifying your Apache Config file

Once you have your files in the right location you can now edit either your `apache.conf` or `httpd.conf` file, depending on your particular installation.

You can find the location to your file with the following.

```bash
$ locate httpd.conf
/usr/local/etc/httpd/httpd.conf
```

If your system returns nothing, run:

```bash
$ locate apache.conf
/usr/local/etc/apache/apache.conf
```

Open the file with your favourite editor.

```bash
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

Comment any `ErrorDocument` directives (e.g. `#ErrorDocument`) and then add your new directives so that your file now looks as follows:

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
ErrorDocument 500 /ErrorPages/500.html
ErrorDocument 501 /ErrorPages/501.html
ErrorDocument 502 /ErrorPages/502.html
ErrorDocument 503 /ErrorPages/503.html
```

Save your file and then test your configuration changes by executing the following.

```bash
$ sudo apachectl configtest
```

If you get any message other than `Syntax OK` then you've done something wrong. You will need to check your changes made to the conf files and see where you may have gone wrong.

The final step is to restart Apache so that it loads your new error pages.

```bash
$ sudo apachectl restart
```

## Minification Setup

As part of the project I have included both the `/src/` and `/dist/` folders. The difference between the two is that the `/dist/` folder contains minified versions of the `/src/` folder files.

There is a `bash` script, found at [/src/scripts/minify][script] which runs the `html` files through `html-minifier` and the `css` files through `postcss`.

### Dependencies

You will need to install both `html-minifier` as well as `postcss` before you can execute the minifaction script.

#### Installing `html-minifier`

The best way to install `html-minifier` is by running the following commands in the project root folder.

```bash
$ cd Apache-Error-Pages/
$ rm -Rf html-minifier/ # ensure you are using the latest version.
$ git clone git://github.com/kangax/html-minifier.git
$ cd html-minifier
$ npm link .
```

#### Installing `postcss`

Once `html-minifier` is installed you can install `postcss` as follows:

```bash
$ npm install cssnano --save
$ npm install postcss-cli --global
```

### Running the minify script

You can run the script with this command:

```bash
$ cd src/
$ ./scripts/minify
```

There are no options for running this script. Executing this command will:

* Delete the `/dist/css/` folder.
* Delete all the error pages with `rm -f ../dist/*.html`.
* Recreate the `/dist/css/` folder.
* Minify the HTML for all files in the `/src/` directory.
* Minify the CSS for all the files in `/src/css/` directory.
* Output the HTML and CSS to the `/dist/` folder.

## Contributing

Please read the [CONTRIBUTING.md][CONTRIBUTING] file for details on how you can get involved in the project as well as the process for submitting bugs and pull requests.

## Code of Conduct

Please read the [CODE_OF_CONDUCT.md][COC] file for the guidelines that govern the community.

## Versioning

We use [Semantic Versioning][semver] for software versions of this project. For a list of all the versions available, see the [tags][tags] and [releases][releases] on this repository.

## Change-Log

View the [`CHANGELOG.md`][changelog] file for a detailed list of changes, along with specific tasks completed for each version released to date.

## Authors

* Justin Hartman - [@justinhartman][author-1]

Also see the list of [contributors][contribs] who have participated in this project.

## TODO

A detailed list of TODO items can be found [over here][todo].

## License

This work is licensed under the [GNU Affero General Public License][agpl]. You can view the full LICENSE by [reading this][license] file.

```text
Copyright (C) 2018 Justin Hartman <justin@hartman.me> (https://justin.hartman.me).

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
* Icons by [Font Awesome][fontawesome] - License [CC BY 4.0][ccby40].
* [html-minifier][html-min] - for compressing the `/src/` html files into the `/dist/` folder. License: [MIT][mit].
* [PostCSS][postcss] - for compressing the `/src/` css files into the `/dist/` folder. License: [MIT][mit].
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
[agpl]: https://opensource.org/licenses/AGPL-3.0
[site]: https://justin.hartman.me
[email]: mailto:justin@hartman.me?subject=Github+Contact
[license]: LICENSE
[404-template]: https://ws2.sinaimg.cn/large/006tKfTcly1fr3klp9lp9g30hs0a1gyv.gif
[todo]: TODO.md
[CONTRIBUTING]: CONTRIBUTING.md
[COC]: CODE_OF_CONDUCT.md
[changelog]: CHANGELOG.md
[semver]: http://semver.org
[tags]: https://github.com/justinhartman/Apache-Error-Pages/tags
[releases]: https://github.com/justinhartman/Apache-Error-Pages/releases
[contribs]: https://github.com/justinhartman/Apache-Error-Pages/contributors
[author-1]: https://github.com/justinhartman
[.github]: https://github.com/justinhartman/.github
[script]: src/scripts/minify
