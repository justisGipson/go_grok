# GO_GROK

Grok/Expose HTTP servers with public URLs – WITH GOLANG

## Build

`$ go build`

## The Stuff

Run the go_grok server. Uses `vcap.me` by default for hostnames, which resolves all subdomains to localhost

```bash
$ ./go_grok
2021/6/3 09:48:22 go_grok server [vcap.me] ready!
```

Now run a local web server, anything running on local is fine.

Then run go_grok as a client by giving it the local port to expose

```bash
$ ./go_grok 8080
port 8080 http available at:
http://y8eyshnpol.vcap.me:9999
```

That address should serve the same content as the local web server on port 8080.

For more fun, run both the client and server with `-p 80`, which will require root to run the server

Uses `qmux` between the client and the server to tunnel subdomain requests down to the client. This is done over a hijacked https connection after a tunnel is established and a new subdomain `vhost` is setup

