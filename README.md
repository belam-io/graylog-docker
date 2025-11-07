# Graylog + OpenSearch Setup Guide

## 1. Copy the Example Environment File

Before making any edits, create your working `.env` file:

```
cp .env.example .env
```

---

## 2. Generate Required Graylog Secrets

Graylog requires two secure values:

* `GRAYLOG_PASSWORD_SECRET` (a long random string)
* `GRAYLOG_ROOT_PASSWORD_SHA2` (a SHA256 hash of your chosen admin password)

### Generate `GRAYLOG_PASSWORD_SECRET`

```
< /dev/urandom tr -dc A-Z-a-z-0-9 | head -c${1:-96};echo;
```

Copy the generated output and paste it into `.env` under `GRAYLOG_PASSWORD_SECRET=`.

### Generate `GRAYLOG_ROOT_PASSWORD_SHA2`

This is your **admin** login password for Graylog.

```
echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
```

Copy the resulting hash and paste it into `.env` under `GRAYLOG_ROOT_PASSWORD_SHA2=`.

---

## 3. Edit and Review `.env`

Open the `.env` file:

```
nano .env
```

Ensure the values look like:

```
GRAYLOG_PASSWORD_SECRET=<your_generated_secret>
GRAYLOG_ROOT_PASSWORD_SHA2=<your_generated_sha256_hash>
OPENSEARCH_INITIAL_ADMIN_PASSWORD=<your_opensearch_password> e.g TestPassword@123
```

Save the file.

---

## 4. Verify and Review `docker-compose.yml`

Open the Compose file and review configuration options:

```
nano docker-compose.yml
```

Ensure services reference environment variables correctly.
Modify settings if required.

---

## 5. Start the Stack

```
docker-compose up -d
```

Check logs:

```
docker-compose logs -f opensearch
docker-compose logs -f graylog
```

Make sure both complete startup successfully.

---

## 6. Access Graylog Web Interface

Open your browser and go to:

```
http://127.0.0.1:9000/
```

**Login Credentials:**

* Username: `admin`
* Password: *the password you entered when generating SHA256*

---

You are now ready to configure inputs, streams, alerts, and dashboards!
