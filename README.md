Hi
你来了!

快走吧. 这玩意没啥用.

https://t.me/mydb_online

https://github.com/dbonline666/dbonline_release/releases

services:
  db_online:
    container_name: db_online
    depends_on:
      postgres:
        condition: service_healthy
    environment:
      - TZ=Asia/Shanghai
    image: dbonline/db_online:latest
    ports:
      - 9090:9090
    restart: unless-stopped
    volumes:
      - ./data:/app/data
      - ./cache:/app/cache
      - ./logs:/app/logs
  postgres:
    container_name: db_online_postgres
    environment:
      - TZ=Asia/Shanghai
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DB=db_online
    healthcheck:
      interval: 10s
      retries: 5
      test:
        - CMD-SHELL
        - pg_isready -U postgres -d db_online
      timeout: 5s
    image: postgres:16-alpine
    restart: unless-stopped
    volumes:
      - ./postgres_data:/var/lib/postgresql/data
      
