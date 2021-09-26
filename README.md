# CommandBlockPermissions

Keep command blocks honest: a player can only save a command in a command block if they are allowed to run that command, so nobody gets around a permission by wiring it to a button.

## How it works

The plugin listens to the `SET_COMMAND_BLOCK` and `SET_COMMAND_MINECART` packets with ProtocolLib. When a player saves a command, its name is looked up in the server command map:

- if the command declares a permission, the player must have that permission;
- otherwise the player must have `cbPerm.<command>`;
- if neither is true, the packet is cancelled and the player is told why, so the command never reaches the block.

An empty command is always allowed, since clearing a command block is harmless.

## Requirements

- Spigot/Paper 1.17 or newer.
- [ProtocolLib](https://github.com/dmulloy2/ProtocolLib), declared as a hard dependency.

## Installation

1. Drop ProtocolLib and the built jar in your server's `plugins/` folder.
2. Restart the server.

## Permissions

| Permission | Description |
| --- | --- |
| `cbPerm.<command>` | Lets the player use `<command>` in a command block, for commands that declare no permission of their own |
| `cbPerm.*` | Lets the player use any command in a command block |

Commands that do declare a permission keep using it, so give the player the permission of the command itself to let them place it.

## Building

```sh
mvn clean package
```

The shaded jar lands in `target/`.
