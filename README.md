Printer Paint
========

A very simple picture-sending application demonstrating how to work with the [Printer API][api].

[Find out more about printers][project page].

Getting started
---------------

This application expects to run on Ruby 1.9.2 or greater.

First, install all the dependencies:

    $ bundle install
    $ bundle exec foreman start

To use this, a printer owner must visit http://localhost:4545/register (or whatever host the application is deployed to). On that page, they should enter a nickname, and the URL endpoint for their printer. For example, the nickname could be `lazyatom`, and the printer URL may be something like http://printer.gofreerange.com/print/1b6c9ad3e1a4d1d34e86f2b550e3a97f.

Then, they can share the url http://localhost:4545/send/lazyatom (or whatever the nickname was) with their friends.

Those friends with the URL can send pictures to the printer by completing the "From" field, scribbling something in the picture canvas and hitting "Send"; the picture will be printed out on the recipient's printer shortly afterwards.


How it works
------------

The Printer ecosystem works by content sources (like this app) sending URLs to a printer URL, which is provided by a [printer backend server][backend]. The Printer backend then requests the page at that URL, renders it and makes it available for the printer identified by that URL.

In this case, when a picture is created, a URL of the form `http://localhost:4545/pictures/:id` is sent to the backend when a picture is created.

This page is styled using the [default `print` stylesheet](http://printer.gofreerange.com/stylesheets/print.css) from http://printer.gofreerange.com, which helps ensure that the layout will work well on the fixed, small width of the printer (384px).

One slight difference between this and the [mail app][] example is that the contents of the drawing canvas are serialised using Javascript, and stored in the database. The page at the `http://localhost:4545/pictures/:id` URL knows how to turn the serialised image data back into the drawing on a canvas.


More background
---------------

Why do I have to enter a printer URL?

Well, the idea is that printers don't all need to be connected to a single central backend server. You can run your own Printer backend server for yourself, or for you and your friends. Or you could run your own backend server behind your firewall. Or you can use a hosted one, like the original server at http://printer.gofreerange.com. It's up to you.

Similarly, many different publishers can be used to send content to a single printer. This demonstration "picture" service isn't tied to any single backend, and you can run your own instance of this publisher yourself too if you like.

[project page]: https://gofreerange.com/printer
[mail app]: https://github.com/freerange/printer-mail
[backend]: https://github.com/freerange/printer
[api]: https://github.com/freerange/printer/wiki/API