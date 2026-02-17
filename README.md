```markdown
# Django HTTP-Only Security Configuration

Secure Django settings for **HTTP-only** deployments (AWS EC2 public IP, internal networks, no SSL).

## Core Settings

## Generate SECRET_KEY

```bash
python3 manage.py shell
>>> from django.core.management.utils import get_random_secret_key
>>> print(get_random_secret_key())
```

```python
# Secret Key (Environment)
SECRET_KEY = os.environ.get("SECRET_KEY")

# Allowed Hosts
ALLOWED_HOSTS = os.environ.get(
    "ALLOWED_HOSTS",
    "localhost,127.0.0.1"
).split(",")

# CSRF Trusted Origins (HTTP)
CSRF_TRUSTED_ORIGINS = os.environ.get(
    "CSRF_TRUSTED_ORIGINS",
    "http://localhost,http://127.0.0.1"
).split(",")
```

## Browser Security Headers

```python
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = "DENY"
```

## Cookie Settings (HTTP-Safe)

```python
SESSION_COOKIE_SECURE = False
CSRF_COOKIE_SECURE = False
```

## HTTPS Disabled

```python
SECURE_SSL_REDIRECT = False
SECURE_HSTS_SECONDS = 0
```


## Deploy Check

```bash
python3 manage.py check --deploy
```

**Status: Secure for HTTP-only deployments**
```



--------------------------------env---------------------

# DJANGO_SETTINGS=http

# SECRET_KEY=(%!va8&o4i*4gbcw%sd^y9&ogza$*1b&i(0s3^23j(b1sl&f^*

# DEBUG=False

# AES_KEY=cf371fae2353d0039c7e951b9efd8b02c1dc334d1e5071c85aed2a3ffee677b2

# ALLOWED_HOSTS=<ip_address>
# CSRF_TRUSTED_ORIGINS=http://<ip_address>

# EMP_ID=MAH001

# DB_ENGINE=django.db.backends.postgresql_psycopg2
# DB_SEG_TOOL=
# DB_USER=
# DB_PASSWORD=
# DB_HOST=<ip_address> or 
# DB_HOST=host.docker.internal
# DB_PORT=5432
