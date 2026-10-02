# CULTIVA+ — Architecture

## 1. System Split

CULTIVA+ separates field intelligence from product/application services.

### Edge domain

Responsible for:

- sensor acquisition
- local decisions
- local persistence
- offline buffering
- HTTP/MQTT publication
- ETL/model workflows

### Application domain

Responsible for:

- authenticated APIs
- relational persistence
- queues/cache
- object storage
- realtime communication
- mobile access

## 2. Data Flow

```text
Sensors
  ↓
Python edge runtime
  ├─→ raw JSONL / CSV
  ├─→ latest snapshot
  ├─→ offline cache
  ├─→ recommendation logic
  ├─→ HTTP ingestion
  └─→ MQTT / IoT path
          ↓
NestJS backend
  ├─→ PostgreSQL
  ├─→ Redis / BullMQ
  ├─→ object storage
  ├─→ Socket.IO
  └─→ mobile client
```

## 3. Offline Resilience

The private edge module contains an offline-cache concept for connectivity loss. This is important in agricultural environments where permanent cloud access cannot be assumed.

## 4. Data Preparation

The edge project includes ETL for:

- CSV agricultural datasets
- locally generated JSONL readings
- curated datasets for training/decision workflows

## 5. Application Stack

The backend package includes NestJS, Prisma, AWS S3 SDK, BullMQ, JWT/Passport, Socket.IO, Swagger, validation, rate limiting, Helmet and metrics-oriented dependencies.

The mobile package is Expo/React Native with navigation, secure storage, notifications, location and realtime-client dependencies.

## 6. Maturity Boundary

Architecture breadth is not the same as production readiness. The native module identifies itself as pre-MVP; this showcase preserves that distinction.
