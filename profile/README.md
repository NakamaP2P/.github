# NakamaP2P TEAM

> **Ecosistema P2P de autocustodia para el intercambio de activos digitales estables en redes EVM.**
>
> Especificaciones primero. Implementaciones después.

---

## ¿Qué es NakamaP2P?

**NakamaP2P** es un ecosistema abierto para facilitar el intercambio **peer-to-peer** de activos digitales en **autocustodia**, con énfasis en **activos estables (stablecoins) sobre redes EVM**.

Nace para dar acceso financiero a ciudadanos de regiones bajo sanciones internacionales —inicialmente **Cuba y regiones similares**— donde los exchanges centralizados no operan, las rampas fiat están bloqueadas y los modelos P2P tradicionales sufren de baja liquidez, primas elevadas y riesgos de contraparte.

El ecosistema se apoya en tres pilares:

- **Pool de liquidez:** los proveedores de liquidez (LPs) stakean stablecoins y actúan como contraparte FIAT.
- **Precios por oráculo con spread fijo:** precio de referencia agregado de fuentes externas y ajustado por balance DeFi; spread configurable del 2.5%.
- **Registro on-chain en HIVE:** trazabilidad canónica de eventos vía `custom_json`, sin costos adicionales y sin dependencia de la integridad de una única stablecoin.

---

## Principios del ecosistema

- **No custodial:** la plataforma nunca controla los fondos en negociación.
- **Liquidez profesional:** los LPs aportan stablecoins al pool y operan dentro de límites AML.
- **Activos admitidos con límites AML:** USDT, USDC y equivalentes admitidos con topes operativos, no excluidos.
- **Autocustodia:** el usuario mantiene el control de sus claves y de sus fondos fuera de las reglas del protocolo.
- **Trazabilidad:** toda operación es auditable y se respalda en HIVE.
- **Gobernanza por LPs:** 1 LP = 1 voto, con cap de stake y KYC-lite.
- **Extensibilidad:** el diseño contempla otros sustratos de liquidación además de EVM.
- **Especificaciones primero:** ninguna implementación se inicia sin artefacto de diseño aprobado.

---

## Flujo de trabajo del ecosistema

```
┌─────────────────────────────────────────────────────────────┐
│  1. ESPECIFICACIONES                                        │
│     Nakama-Protocol (fuente de verdad del diseño)           │
│     Visión · Dominio · Precios · Liquidez · AML · Estados   │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          │ Deriva
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  2. IMPLEMENTACIONES                                        │
│     Contratos · Backend · Frontend · SDKs · Tools · Scripts │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          │ Integra
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  3. OPERACIÓN                                               │
│     Despliegue · Monitoreo · Gobernanza · Soporte           │
└─────────────────────────────────────────────────────────────┘
```

**Regla del ecosistema:** ningún repositorio de implementación introduce lógica que no esté definida en `Nakama-Protocol`. Toda divergencia se documenta como ADR en el repositorio de especificaciones antes de implementarse.

---

## Repositorios del ecosistema

### 📐 Especificaciones (fuente de verdad)

| Repositorio | Descripción | Estado |
|---|---|---|
| **[Nakama-Protocol](https://github.com/NakamaP2P-TEAM/Nakama-Protocol)** | Diseño y artefactos del protocolo: visión, dominio, precios, liquidez, compliance AML, máquina de estados, reglas de negocio, disputas, reputación, amenazas, registro HIVE, ADRs y diagramas. **Sin implementación.** | 🚧 v0.1 en curso |

### ⚙️ Implementaciones

| Repositorio | Descripción | Deriva de |
|---|---|---|
| **Nakama-Contracts** | Contratos inteligentes del protocolo en redes EVM (Polygon, RSK). Incluye pool de liquidez, escrow, registro de activos y reputación on-chain. | `Nakama-Protocol` |
| **Nakama-Backend** | API y lógica de gestión: anuncios, registro dual, reputación, integración con HIVE (`custom_json`), oráculos y web3. | `Nakama-Protocol` |
| **Nakama-Frontend** | Interfaz web SPA/PWA: tablón de anuncios, flujo de compra/venta, panel del LP, panel del administrador y gobernanza. | `Nakama-Protocol` |
| **Nakama-SDK** | SDKs cliente para integrar el protocolo desde aplicaciones de terceros. | `Nakama-Protocol` |

### 🛠️ Herramientas y operación

| Repositorio | Descripción |
|---|---|
| **Nakama-Tools** | Utilidades, CLI y scripts de apoyo (verificación de estado, auditoría de eventos HIVE, simulaciones de precios). |
| **Nakama-Scripts** | Scripts de despliegue, migración, sincronización de ABIs y operación. |
| **Nakama-Infra** | Configuración de infraestructura, monitoreo y observabilidad (sin secretos). |


## Cómo contribuir

1. **Lee primero las especificaciones.** Todo cambio de comportamiento empieza como propuesta en `Nakama-Protocol` (ADR o NKP).
2. **Sigue el código de conducta** del repositorio `.github`.
3. **Usa las plantillas** de issues y pull requests.
4. **Reporta vulnerabilidades** de forma privada según `SECURITY.md`.
5. **No incluyas secretos** (claves, RPCs privadas, datos personales) en ningún repositorio.

La guía completa está en [`.github/CONTRIBUTING.md`](https://github.com/NakamaP2P-TEAM/.github/blob/main/CONTRIBUTING.md).

---

## Seguridad

- **No custodial por diseño.** La plataforma nunca controla fondos de usuarios ni de LPs fuera de las reglas del protocolo.
- **Registro canónico en HIVE.** La trazabilidad no depende de la integridad de una única stablecoin.
- **Activos con `freeze` admitidos bajo límites AML,** con mitigaciones de diseño frente a la captura técnica.
