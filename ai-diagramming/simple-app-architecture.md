# Simple App Architecture

Mermaid type: `architecture-beta` (beta). Shows web and mobile clients, an API gateway, the backend API, and a primary database with two read replicas.

```mermaid
architecture-beta
    group app(cloud)[Simple app]

    service web(mdi:laptop)[Web client] in app
    service mobile(mdi:cellphone)[Mobile client] in app
    service gw(logos:aws-api-gateway)[API gateway] in app
    service api(server)[App API] in app
    service db(database)[DB primary] in app
    service rep1(database)[DB replica 1] in app
    service rep2(database)[DB replica 2] in app

    align row web mobile
    align row rep1 db rep2

    web:B --> T:gw
    mobile:B --> T:gw
    gw:B --> T:api
    api:B --> T:db
    db:L --> R:rep1
    db:R --> L:rep2
```

## Legend

| Icon | Name in code | Meaning |
|---|---|---|
| Laptop | `mdi:laptop` | Web client (browser) |
| Cellphone | `mdi:cellphone` | Mobile client |
| API gateway | `logos:aws-api-gateway` | Single entry point for clients |
| Server | `server` | Backend API |
| Database | `database` | Primary database and read replicas |

Edges from the primary to the replicas show data replication.

## Notes

- Both clients call the API gateway, which routes requests to the App API.
- The App API writes to the primary database. The replicas receive replicated data.
