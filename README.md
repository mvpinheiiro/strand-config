# Strand Config

Configuração de badges do aplicativo **Strand** para os streams formatados pelo AIOStreams.

## Importação

Cole no Strand a URL RAW:

https://raw.githubusercontent.com/mvpinheiiro/strand-config/main/badge/badges.json

## Regras

- **54 badges em 7 grupos**: Destaques, Fonte e qualidade, Resolução, Vídeo, Áudio, Canais e Idiomas.
- **Fonte e qualidade**: 20 badges originais de REMUX (T1–T3), BLU-RAY (T1–T8) e WEB (T1–T6), com os três `Unranked` desativados; as identificações agora dependem dos marcadores das *ranked stream expressions* (`stream.rseMatched`), não da interpretação dos nomes dos arquivos. Os tiers BD T1–T8 abrangem animes.
- **Resolução**: 2160p (`#4K`), 1080p (`#FHD`), 720p (`#HD`), mostrando somente a maior delas.
- **Vídeo**: somente a melhor faixa encontrada: `DV > HDR10+ > HDR10 > HDR`. `HDR10` é a hashtag complementar emitida pelo formatter; `SDR` não recebe badge. `IMAX Enhanced` ou `IMAX` pode aparecer como badge adicional, mas não simultaneamente.
- **Áudio**: `DD+ ATMOS` e `TrueHD ATMOS` usam exclusivamente hashtags das RSEs. Ambas podem aparecer simultaneamente. Outros codecs são ocultados quando existe uma delas; caso contrário, só aparece o codec de maior prioridade.
- **Canais e idiomas**: exibidos todos os valores distintos que chegarem como `#CH_*` e `#LANG_*`. Sem idioma latino.
- **Apple TV Top**: precisa de `#DV` e `#DD+ ATMOS` simultaneamente; sem requisito de 4K. O marcador `DV (Disk)` não se confunde com `DV`.
- **SeaDex Release**: `#SeaDex Best` ou `#SeaDex Alt`.
- Não há detecção adicional de Atmos ou fallback para animes. Os badges dependem dos marcadores presentes no formatter.

## Arquivos

- `badge/badges.json`: configuração principal importada pelo Strand.
- `badge/logo/`: imagens Dolby usadas por alguns badges.

Os ícones já existentes foram preservados. Para `IMAX Enhanced`, a configuração utiliza um PNG público do repositório `leonevz/Elite-Badges`.

## Atualização

O endereço de importação é fixo, pois aponta para `main`. Se o Strand armazenar a configuração em cache, pode ser necessário atualizar/reimportar o JSON.

## Verificação

As regex passaram por 15 cenários simulados, incluindo DV + dois Atmos simultâneos, priorização HDR, codecs, IMAX, múltiplos canais e SeaDex. É recomendável validar a exibição dentro do Strand com streams reais.
