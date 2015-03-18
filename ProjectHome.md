# What is it? #

PixiClock is tiny desktop clock widget for true geeks.

It use original pixi-icons instead digits and show ordinary digits only as hint, when mouse comes over.

You can get [more information about pixi-culture](http://goglus.com/), and [view more pixi "urods"](http://goglus.com/pixel/urod.htm).

# Features #

  * Excentric and ascetic design
  * Build-in alarm clock
  * Snap-to-border support
  * Hints
  * Flexible control by external applications
  * Skins
  * Easy installation and configuration

# Installation #

## Requirements ##

You need:

  * Python
  * Python Tk extension

You can check it by command:

```
$ python -c 'import Tkinter; print "OK"'
```

If you get "OK" message -- be sure of this.

If you get message like this:

```
ImportError: No module named Tkinter
```

you need to install python-tk extension.

## Standard installation way ##

You can use native Python installation procedure:

```
$ wget http://pixiclock.googlecode.com/files/pixiclock-0.2.0.tar.gz
$ tar xzf pixiclock-0.2.0.tar.gz
$ cd pixiclock-0.2.0
$ python setup.py build
$ sudo python setup.py install
```

You can install PixiClock with prefix:

```
$ sudo python setup.py install --root /opt
```

## Hackers way ##

True hackers can install PixiClock manualy.

Just get and unpack sources, open file `pixiclock` in
your favorite editor, edit the first line (it begins with "#"), and other lines if you need. Now copy file wherever you want in your system.
You can install `pixiclock-client` the same way.

# Usage #

## Quickstart ##

Just start pixiclock:

```
$ pixiclock
```

Start as alarm clock (at 9:00 and 17:00):

```
$ pixiclock -a 9:00 -a 17:00
```

Load external skins (see root-menu/Skins):

```
$ pixiclock -f skins/tiny.ini
```

Start as diemon:

```
$ pixiclock -d
```

## Options ##

```
-v
    print version
-h
    print help message
-p PORT
    run pixiclock in network mode on PORT; try
    $ pixiclock-clietn -p PORT "TEST"
-n
    same as -p 7070
-a HH:MM
    set up alarm; can be used many times
-a HH:MM@/path/command
    set up alarm and command to execute on it
    (there is no way to pass arguments to command yet)-f FILE
    load skin from configuration file;
    can be used many times to load diferent
    skins in conjunction
-c COMMAND
    piped watchdog command
-w
    do not ignore window manager
-d
    daemonize
```

## IPC modes ##

Pixiclock can notify you about any events. You
can control it due to pipes or network.

### Piped watchdog scope ###

You can write a program that periodically produces data to standard output.
It may look like this:

```
#!/bin/sh
# file /home/xxx/example.sh
LANG=C
while : # infinite loop
do
  # we emit control words and text to display (date)
  echo 'BG=#ff0000 FG=#ffff00 GEOMETRY=+30+30 DELAY=1000'
  date
  # and sleep 10 seconds
  sleep 10
done
```

Now you can run the pixiclock and tell it to use this data provider.

```
pixiclock -c /home/xxx/example.sh
```

You can see date message every 10 seconds.

### Network scope ###

You can communicate with pixiclock via a network connection.

Run the pixiclock in network mode:

```
$ pixiclock -n -d
```

Use `pixiclock-client` to send messages to `pixiclock`:

```
$ pixiclock-client 'OK!'
$ pixiclock-client 'BG=#770000;FG=#ffffff;RED OK!'
$ date | pixiclock-client
```

Under the agreement, the `pixiclock` and `pixiclock-client` uses
port 7070. You can specify an alternate port. Use the
option `-p N`.

### Control words ###

As you can see above, message may contain control words.
Control words are separate by space chars or ';' sign.
You can specify colors, places, and time delays. Examples:

```
BG=#ff0000 -- red backgound
FG=#00ff00 -- green foreground
DEALY=1000 -- delay one second
GEOMETRY=+10-10 -- place near left-bottom corner of screen
```

### Demos ###

You can find more eamples in `demos/`.

# Authors #

Code writen by Michurin Alexey <a.michurin@gmail.com>.

The original concept and graphic design belongs to Mihail Razuvaev (goglus) <goglus@gmail.com>.

# Enjoy! #