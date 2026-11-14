
### 1. `dig`

```bash
dig example.com

# Только IP-адреса
dig +short example.com A

# IPv6
dig +short example.com AAAA
```

### 2. `nslookup`

```bash
nslookup example.com
```

### 3. `host`

```bash
host example.com
```

### 4. Через системный DNS Ubuntu

```bash
getent ahosts example.com
```

### 5. Проверить конкретный DNS-сервер

```bash
# Google DNS
dig @8.8.8.8 +short example.com

# Cloudflare
dig @1.1.1.1 +short example.com
```