# Connection
**Login name format**
```bash
user@domain
```

## ssh
Securely connects to hostname and executes command.

If command ommited, simply connects to the host.

```bash
ssh <hostname> <command>
```

**Login name & port**
```bash
ssh -l <name> -p <port> <hostname> <command>
```

**Tunneling**
```bash
ssh -L <port>:localhost:<port> <hostname> <command>
```

## scp
Copies file from source to destination securely.

```bash
scp <source> <destination>
```

**Directory**
```bash
scp -r <source> <destination>
```