# Graylog Docker (simple template)

Single-machine Graylog + OpenSearch + MongoDB for development / learning.

Quick steps:
1. Copy .env.example -> .env and fill secrets.
2. Ensure vm.max_map_count >= 262144: sudo sysctl -w vm.max_map_count=262144
3. Start: ./start.sh (or docker compose up -d)
4. Open Graylog UI at the value in GRAYLOG_HTTP_EXTERNAL_URI (default http://127.0.0.1:9000/)

Security: Do NOT commit .env to GitHub.
