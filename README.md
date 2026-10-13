# Strand Config

Configuração de badges para o aplicativo Strand.

## Importação

Use no Strand a URL RAW:

https://raw.githubusercontent.com/mvpinheiiro/strand-config/main/badge/badges.json

## Conteúdo

- `badge/badges.json`: 55 filtros organizados em 7 grupos.
- 20 tiers de fontes: REMUX 1–3 e Unranked; BLU-RAY 1–8 e Unranked; WEB 1–6 e Unranked.
- Vídeo e formatos HDR em amarelo; áudio e canais em branco; resolução com gradação 2160p (amarelo), 1080p (laranja) e 720p (vermelho).
- 12 badges de idioma preservados.
- DD+ Atmos e TrueHD Atmos em badges separados.
- IMAX Enhanced e categorias antigas Best, Good e OK removidos.
- `badge/logo/`: cinco logotipos Dolby personalizados, em PNG transparente, preto, com 124 px de altura.

Os padrões regex dos tiers seguem a configuração de referência `Other/fusion-tags-ume.json` de `nobnobz/Omni-Template-Bot-Bid-Raiser`. Os badges Dolby especializados e os idiomas preservam suas regras anteriores.

Ao editar `badge/badges.json`, a URL de importação continua a mesma.
