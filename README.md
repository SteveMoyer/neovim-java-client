# Neovim Java Client

Wrapper around the neovim message pack api to talk to a neovim process.
This is a WIP lots of functions do not have wrappers yet.

## Usage

Standard usage would be to create a connection to a neovim instance.
There are two provided connection types.

- SocketNeovim
    - Connection to a socket of the form address:port.
    - This is **NOT** a connection to a UNIX socket.
```java
MessagePackRPC.Connection connection = new SocketNeovim("127.0.0.1:6666");
```
- EmbeddedNeovim
    - Connection to an embedded neovim launched with the --embed flag
```java
MessagePackRPC.Connection connection = new EmbeddedNeovim("nvim");
```

Once you have a connection you can create a Neovim instance that will talk to the connected neovim instance.

```java
try (Neovim neovim = new Neovim(connection)) {
    <use neovim>
}
```

## Notes

UNIX domain sockets are not supported out of the box by this library.
These sockets are not supported by the SDK and require JNI code to use.
There are libraries that provide this support and you can wrap the resulting socket in a `MessagePackRPC.Connection`
