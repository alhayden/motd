# motd
simple terminal greeter

## Use
Place your `.WELCOME` configuration file in your homedir.
Run `motd` from your `.shellrc` to recieve a greeting each time you open a terminal

## Configuration
The messages that motd sends are defined by the user in their `.WELCOME` file.  The file contains these parts (see the example `.WELCOME` in this repo):


The root contains two objects:
 - `header` - the message to be sent at the top of each motd.  It replaces `%host` with this machine's hostname, `%user` with the current user, and `%date` with the current date
 - `notifications` - an array of all the notifications


Each `notification` contains these values:
 - `name`: the name of this notification (required, but is not displayed)
 - `msg` : optional text to wrap around the notification, `%s` is replaced with the displayed text
 - `type`: the type of this notification, can be `reminder`, `splash`, `random`, or `always`.
 - `ansi`: optional ansi codes, formatted like {"r":`r`, "g":`g`,"b":`b`, "codes":[`1`, `2`]}


`reminder`s include:
 - `warnings`: an optional array of numbers representing the days before each event to send a reminder; defaults to just 0 (day-of)
 - `strp`, the format to parse times, see https://docs.python.org/3/library/time.html#time.strftime
 - `values`: a map of dates (in the form specified by `strp`) pointing to the message to be sent when that date is selected by `warnings`


`random`s and `splash`s include:
 - `null_chance`: the chance to send no message at all
 - `values`: an array of strings to be sent, picked randomly


`random` notifications are consistent throughout each day, while `splash` notifications vary every time `motd` is run.


`always` notifications always display

`header` notifications always display and are **not** preceeded by bullet points

`separator`s are simply horizontal lines

`url`'s request and return the utf-8 encoded result of a request to the `url` field

**See the `.WELCOME` file in this repository as an example**
