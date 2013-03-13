All Files are Copyright 2012 Nate Finch, please do not copy or distribute

This is a MUD (http://en.wikipedia.org/wiki/MUD) written in the Go programming language.

*** Currently implemented ***

- Logging in (any username or password will work, but simultaneous logins with duplicate names will be prevented)
- Movement (8 compass directions plus up and down)
- smile (an emote that can be targetted at no one, yourself, or someone else
- quit
- look (or l) shows the room contents (though you can't look *at* something yet)
- say
- tell
- The world is an autogenerated 10x10 square. Boring, but it's a good test bed
- multiple users can connect and interact
- will run using all currently available CPUs as necessary

*** Implementation notes ***

- There are no locks per se.  Concurrency is handled by goroutines communicating via channels.
- In the case of needing to modify two objects synchronously, we always modify the one with the lower Id first (a version of lock ordering) to prevent deadlocks
- There are no tests yet (boo!) but they're next on the list

 
*** To build and run ***

navigate to /main
go build natemud.go  (builds if you have go installed)
natemud.exe  (runs current executable)

This will run the mud on port 8888 of your current machine. To change the port, use -p <port>

*** Bugs ***

The mud currently assumes line endings are always \r\n. If your telnet client only sends \n, then you'll lose the last character of any input.  If your telnet client sends something else entirely, then it just won't work.

Connecting with PuTTY in Telnet mode sends some garbage characters initially.. I haven't yet put time into figuring out how to handle those correctly. If you use PuTTY, choose "raw" as the connection type, and it'll work fine. Windows telnet works fine. I haven't tried other telnet clients.

I'm sure there's other problems that I haven't found yet.  Use at your own risk, etc.
