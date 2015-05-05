# Encoding subjects in emails

During our work with integrating inbound mailing from users into app-specific inbox, we bumped into problem of encoding subjects and attachments file names depending on the characters it includes. Standard of email messaging does not accept non-ASCII chars, therefore the environment of sender and receiver has to encode and decode it properly.

It turns out that it may be done in one of these two ways:
* [Quoted Printable](http://en.wikipedia.org/wiki/Quoted-printable) (starts with "=?utf-8?Q")
* [Base64](http://en.wikipedia.org/wiki/Base64) (starts with "=?utf-8?B")

Regarding Ruby environment, we used [Griddler gem](https://github.com/thoughtbot/griddler) for processing mails. Even though it processed subjects properly, it leaves the attachments as is making us decode the filename by us. Using [mail gem](https://github.com/mikel/mail) and its `Mail::Encodings.unquote_and_convert_to` method let you decode attachment file properly.

More to read:
* [Great answear from SO](http://stackoverflow.com/questions/454833/system-net-mail-and-utf-8bxxxxx-headers)

