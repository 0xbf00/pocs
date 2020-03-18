# No `dyld`, No Sandbox

Proof of concept project showing that sandbox initialisation does not happen for statically linked binaries, even if the target program includes sandboxing entitlements and is properly code-signed.

Note: `unsandboxed-bin` is a binary file generated using a modified version of [stek29's `minmacho`](https://github.com/stek29/minmacho) tool. The changes I've made to stek29's project are fairly minor. Because I haven't gotten around to cleaning them up, I am including the binary only.

Using `otool`, you'll see the program is just running in an infinite loop:

```sh
$ otool -tv unsandboxed-bin 
unsandboxed-bin:
(__TEXT,__text) section
000000000000174d	nop
000000000000174e	jmp	0x174d
# Lots of other output due to padding added to file
```

## Building

Modify `src/Makefile` to use your signing identity. Then invoke `make` in the `src/` directory.

To verify that the resulting `unsandboxed-poc` is indeed running unsandboxed, use `Activity Monitor.app` or `asctl` while running the program. `asctl` will let you know that the app is signed with App Sandbox entitlements

```sh
$ asctl sandbox check --file unsandboxed-poc 
/Users/jakob/unsandboxed-poc:
	signed with App Sandbox entitlements
```