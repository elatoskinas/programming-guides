# Connection
**Login name format**
```bash
user@domain
```

## ssh
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
```bash
scp <source> <destination>
```

**Directory**
```bash
scp -r <source> <destination>
```