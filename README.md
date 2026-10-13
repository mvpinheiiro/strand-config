# Strand Config — badges para AIOStreams

Configuração de badges do **Strand** para streams exibidos pelo formatter personalizado do **AIOStreams / Tamtaro + Vidhin**.

## Importar no Strand

**URL RAW**:

https://raw.githubusercontent.com/mvpinheiiro/strand-config/main/badge/badges.json

O arquivo tem **54 badges, todos habilitados**, organizados em 7 grupos na seguinte ordem:

1. Destaques
2. Fonte e qualidade
3. Resolução
4. Vídeo
5. Áudio
6. Canais
7. Idiomas

## Comportamento

### Fonte e qualidade

- **REMUX**: T1–T3 e Unranked.
- **Blu-ray**: T1–T8 e Unranked; T4–T8 existem para classificações adicionais de anime provenientes das expressões de Vidhin. Filmes e séries tradicionais normalmente usam apenas T1–T3.
- **WEB**: T1–T6 e Unranked; T4–T6 são usados por classificações adicionais de anime.
- Os níveis usam somente os marcadores das expressões ranqueadas presentes em `stream.rseMatched`, e não analisam grupos de release no nome do arquivo.
- Os badges **Unranked** exigem, respectivamente, `#SRC_REMUX`, `#SRC_BLURAY` ou `#SRC_WEB`, **sem qualquer marcador reconhecido de nível T1–T8**. Por isso, a configuração **requer o complemento do formatter** indicado abaixo.

### Vídeo e resolução

- Resolução: somente uma dentre `#4K` / `#FHD` / `#HD`, com prioridade da maior.
- Vídeo: somente a mais prioritária dentre `#DV`, `#HDR10+ Boost`, `#HDR10`, `#HDR`.
- `#DV (Disk)` não equivale a `#DV`.
- **IMAX Enhanced** e **IMAX**: logos pretos, apenas um deles visível se ambos forem sinalizados.
- Não há badge para SDR.

### Áudio

Exibição dos badges em ordem, agrupando **Dolby antes de DTS**:

1. TrueHD Atmos
2. DD+ Atmos
3. TrueHD
4. Dolby Digital+
5. Dolby Digital
6. DTS:X
7. DTS-HD MA
8. DTS-HD
9. DTS

Os badges Atmos dependem somente das expressões `#TrueHD ATMOS` e `#DD+ ATMOS`; ambos podem aparecer no mesmo stream. Os codecs comuns continuam com as regras de exclusividade preexistentes (somente o codec prioritário quando não há Atmos). A ordem visual Dolby/DTS **não altera a precedência técnica das regex dos codecs**.

### Canais, idiomas e destaques

- Canais: todos os canais sinalizados (`#CH_71`, `#CH_61`, `#CH_51`).
- Idiomas: todos os disponíveis, nesta ordem: **PT, EN, ES**, DE, FR, HI, IT, JA, KO, RU, ZH.
- Apple TV Top: `#DV` junto de `#DD+ ATMOS`, sem exigência de 4K.
- SeaDex: `#SeaDex Best` ou `#SeaDex Alt`.

## Complemento necessário no formatter do AIOStreams

No fim do campo **Description** do formatter personalizado, acrescentar **exatamente**:

```text
{stream.quality::in('BluRay REMUX','DVD REMUX')[" #SRC_REMUX"||""]}{stream.quality::in('BluRay')[" #SRC_BLURAY"||""]}{stream.quality::in('WEB-DL','WEBRip')[" #SRC_WEB"||""]}
```

Isso acrescenta apenas hashtags de fonte à descrição, preservando o restante do formatter e **sem exibir o nome do arquivo**.

**Atenção:** sem esse complemento, os novos badges Unranked estarão habilitados, mas **não aparecerão**, porque o JSON não reconstrói a fonte por conta própria. É necessário que `stream.quality` forneça uma qualidade compatível com esses valores; confirme no Preview do AIOStreams.

As demais hashtags continuam vindo de `stream.rseMatched`, com os complementos `#HDR10`, `#LANG_*` e `#CH_*` já existentes no formatter personalizado.

## Imagens IMAX

As duas imagens pretas são arquivos públicos existentes no repositório [kingsizew/badges](https://github.com/kingsizew/badges), em `badge-images/imax/`. Outros ícones já existentes foram preservados.

## Validação

- 54 badges com `isEnabled: true`.
- 25 testes de correspondência de regex aprovados, incluindo tiers, Unranked, IMAX, idiomas e coexistência dos dois Atmos.
- A compatibilidade visual definitiva ainda precisa ser verificada dentro do Strand e a emissão de `#SRC_*` no Preview do AIOStreams.

Se o Strand armazenar badges em cache, reimporte a URL RAW após a atualização.
