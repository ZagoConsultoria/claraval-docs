# API - Live Streaming

**Prefixo:** `/live`
**Autenticação:** Requerida (exceto HLS proxy)

## Arquitetura

```
OBS Studio (RTMP :1935) → MediaMTX → HLS → Backend (proxy) → Frontend (hls.js)
```

## Endpoints

### GET /live/status

Retorna se há live ativa.

**Response (200):**

```json
{
  "online": true,
  "streamUrl": "/live/hls/stream/index.m3u8"
}
```

### GET /live/hls/{path}

Proxy para o stream HLS do MediaMTX. **Público** (autenticação via frontend).

O backend faz proxy das requisições HLS para o MediaMTX, evitando expor o MediaMTX diretamente.

### POST /admin/live/start

Marca a live como ativa. **Admin only.**

### POST /admin/live/stop

Marca a live como inativa. **Admin only.**

## Frontend

- Player customizado com hls.js na identidade visual Claraval
- Indicador "AO VIVO" na seção e-learning quando live ativa
- Controles: play/pause, volume, fullscreen
- Apenas usuários autenticados podem acessar

## Configuração do MediaMTX

Arquivo `mediamtx.yml` na raiz do repositório backend:

- Recebe RTMP na porta 1935
- Converte para HLS automaticamente
- Capacidade: ~30 espectadores simultâneos
- Gerenciado via NSSM como serviço Windows
