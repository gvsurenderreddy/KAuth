KAuth
https://github.com/korylprince/KAuth

#Installing#

This has been installed on various types of servers. It should work on any machine as long as it is running a webserver and PHP (5+).

If you are using the ldap_ad\ extension you will need php-ldap.

Simply copy the KAuth folder to your web directory and copy auth/options.php.def to auth/options.php and edit it for authentication options.

Also included are three files, dl.list.def, al.list.def, and users.list.def. These files are examples for the al, dl, and password\_file libraries. To use them copy them to al.list, dl.list, or users.list and enable the libraries in options.php.

There is a simple interface for testing logins included. Just visit your website with the correct directory.

If you have any issues or questions, email the email address below, or open an issue at:
https://github.com/korylprince/KAuth/issues

#Usage#

This distribution attempts to be a set of extensible, modular libraries that authenticate users.
authlib.php is the main library that takes an array of types and options. It then calls a library for each of the types.

Libraries take the form of auth\_libraryname.php. The library must contain a function named libraryname\_auth that takes the variables $username, $password, and $options.

Each library must return an array with key "Login" that has a value of "Fail","Server","Restricted","True", or "None". They may also return data with key "data" and an array of key/value pairs and flags with key "flags" and an array of values.
Example:

{"Login":"True","data":{"timeLeft":598},"flags":["noPassword"]}

A key of "errorCode" may be returned if "Login" is "Fail","Server", or "Restricted".
Example:

{"Login":"Server","errorCode":"ldap_ad_3","flags":[]}

This distribution contains an example login handler (login.php), a set of all options available (options.php.def) and a simple web interface for testing purposes.

Also included is a utility (auth/mkpasswd.php) to generate password hashes for the password_file library. Use like:

**$ php mkpassword.php password**

For instance:

**$ php mkpassword.php admin**

would output:

3669ff21deff9abcc47fefb2d39a30c8

and you would put:

{"administrator":"3669ff21deff9abcc47fefb2d39a30c8"}

in auth/users.list to allow administrator to log in with password admin.

Included libraries are:

ldap\_ad (Active Directory), al (Access List - JSON encoded file with usernames), dl(Deny List - JSON encoded file with usernames), password\_file (JSON encoded file with username / password hash), session (Use PHP sessions to only allow login session), and admincheck (returns an admin flag if administrator is username.)

#Copyright Information#

jsmin.js is Public Domain code produced by Douglas Crockford: http://www.json.org/

jQuery and jQuery UI are produced by the jQuery team: http://jquery.com/ and http://jqueryui.com/

session_lib.php was taken from the PHP manual: http://php.net/manual/en/function.session-set-save-handler.php

All other code is Copyright 2012 Kory Prince (korylprince at gmail dot com.) This code is licensed under the GPL v3 which is included in this distribution.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

