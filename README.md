# Hackathon Starter

A Dockerized setup for hackathon projects with PostgreSQL, MinIO, and Nginx.

## Setup

1. **Clone Repo**:
   ```bash
   git clone https://github.com/MrDrtyui/hackathon-deploy-default.git
   cd hackathon-deploy-default
   ```

2. **Set Environment**:
   Create `.env.postgres`:
   ```bash
   POSTGRES_USER=your_user
   POSTGRES_PASSWORD=your_password
   POSTGRES_DB=your_database
   ```

3. **Run Services**:
   ```bash
   docker-compose up -d
   ```

4. **Access**:
   - PostgreSQL: `localhost:5433`
   - MinIO: `localhost:9001` (user: `minio`, pass: `minio123`)
   - Nginx: `http://localhost`

5. **Stop Services**:
   ```bash
   docker-compose down
   ```

## Services

- **PostgreSQL** (`postgres:16`):
  - Port: `5433` (maps to `5432`)
  - Volume: `postgres-data`
  - Env: `.env.postgres`
  - Memory: 512MB

- **MinIO** (`minio/minio`):
  - Ports: `9000` (API), `9001` (console)
  - Bucket: `tickets`
  - Volume: `./minio/data`
  - Memory: 512MB

- **Nginx** (`nginx:alpine`):
  - Port: `80`
  - Config: `./nginx.conf`
  - Routes: `/public/` → MinIO, `/api/` → `api:3000`
  - Memory: 512MB

## Notes
- Update `drtyui.ru` in `nginx.conf` for your domain.
- API backend (port `3000`) not included; add it to `docker-compose.yml` if needed.
- Run `git pull origin main` before pushing to avoid conflicts.

## License
MIT License
