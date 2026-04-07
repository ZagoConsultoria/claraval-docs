# API - Live Streaming

**Prefixo:** `/live`
**Autenticacao:** Requerida (exceto HLS proxy)

## Arquitetura

```
OBS Studio (RTMP :1935) → MediaMTX → HLS → Backend (proxy) → Frontend (hls.js)
```

## Endpoints

### GET /live/status

Retorna se ha live ativa.

**Response (200):**

```json
{
  "online": true,
  "streamUrl": "/live/hls/stream/index.m3u8"
}
```

### GET /live/hls/{path}

Proxy para o stream HLS do MediaMTX. **Publico** (autenticacao via frontend).

O backend faz proxy das requisicoes HLS para o MediaMTX, evitando expor o MediaMTX diretamente.

### POST /admin/live/start

Marca a live como ativa. **Admin only.**

### POST /admin/live/stop

Marca a live como inativa. **Admin only.**

## Frontend

- Player customizado com hls.js na identidade visual Claraval
- Indicador "AO VIVO" na secao e-learning quando live ativa
- Controles: play/pause, volume, fullscreen
- Apenas usuarios autenticados podem acessar

## Configuracao do MediaMTX

Arquivo `mediamtx.yml` na raiz do repositorio backend:

- Recebe RTMP na porta 1935
- Converte para HLS automaticamente
- Capacidade: ~30 espectadores simultaneos
- Gerenciado via NSSM como servico Windows
