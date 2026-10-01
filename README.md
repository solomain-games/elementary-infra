# Elementary — инфраструктура

Окружения проекта **Elementary**: локальное для разработки (`local/`), позже боевое (`prod/`).

## Локальное окружение

Требуется Docker Desktop.

```powershell
cd local
docker compose up -d
docker compose ps
```

| Сервис | Адрес | Назначение |
|---|---|---|
| Redis | `localhost:6379` | состояние комнат и партий |
| Redis Insight | http://localhost:5540 | просмотр содержимого Redis |

Подключение к Redis в Redis Insight: host `redis`, port `6379` (Redis Insight работает в той же сети Docker и обращается к Redis по имени сервиса).

Redis запущен с AOF (`appendonly yes`), данные хранятся в томе `redis-data` и переживают перезапуск и пересоздание контейнера.

| Команда | Что делает |
|---|---|
| `docker compose up -d` | поднять всё в фоне |
| `docker compose ps` | статус сервисов |
| `docker compose logs -f redis` | логи Redis |
| `docker compose exec redis redis-cli` | консоль Redis |
| `docker compose down` | остановить и удалить контейнеры, тома сохраняются |
| `docker compose down -v` | то же и **удалить данные** |

Позже здесь появятся PostgreSQL и RabbitMQ (этап 2).
