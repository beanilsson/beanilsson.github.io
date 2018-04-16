# Hello Server!
After learning the very basics of how to write, compile and run a Crystal program. It's time to crank it up a notch by writing our own HTTP server.
So create a file named `server.cr` and start typing!
To create a server, we first need to `require` the `http/server` class. This allows us to use the `HTTP` module along with the `Server` implementation. For more information about requiring files, (read here.)[./requiring.md]
```
require "http/server"
```

```

server = HTTP::Server.new(3000) do |context|
  context.response.content_type = "text/plain"
  context.response.print "Hello world, got #{context.request.path}!"
end

puts "Listening on http://127.0.0.1:3000"
server.listen

```

*Note: If you run Crystal from a Vagrant box you need to a non-localhost bind address.*
```
require "http/server"

server = HTTP::Server.new("0.0.0.0", 3000) do |context|
  context.response.content_type = "text/plain"
  context.response.print "Hello world, got #{context.request.path}!"
end

puts "Listening on http://0.0.0.0:3000"
server.listen

```
