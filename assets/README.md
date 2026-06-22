# assets — FinHire

Arte da marca usada na landing page. **A logo no site hoje é desenhada em CSS**
(monograma FH + wordmark FinHire), então a página já sobe bonita sem depender
de imagem. Os arquivos abaixo são os "slots" pra quando a arte/foto chegar.

## O que subir (e com qual nome EXATO)

| Arquivo | Onde aparece | Status |
|---|---|---|
| `favicon.svg` | Aba do navegador | ✅ placeholder (monograma FH) — trocar pelo ícone final |
| `sandro.jpg` | Bloco "Quem está por trás" — **foto de TERNO** | ⬜ subir — cai em fallback "SV" se ausente |
| `rodrigo.jpg` | Bloco "Quem está por trás" — **foto de POLO** | ⬜ subir — cai em fallback "RA" se ausente |
| `og.png` | Preview ao compartilhar o link (1200×630) | ⬜ recomendado pra WhatsApp/redes |
| `logo-dark.png` / `logo-light.png` | (opcional) trocar a logo CSS por PNG | ⬜ opcional |

> ⚠️ **Confirmar:** assumi que a foto de **terno = Sandro** e a de **polo = Rodrigo**.
> Se for o contrário, basta inverter os nomes dos arquivos ao subir.

### Como subir as fotos (rápido, pelo navegador)
1. Abrir `https://github.com/rodrigoarboes/finhire/upload/claude/beautiful-goldberg-t8osfx/assets`
2. Arrastar `sandro.jpg` e `rodrigo.jpg` (foto quadrada, ~600×600 ou maior)
3. Commit → o deploy re-roda sozinho e as fotos aparecem.

## Paleta provisória (no feeling — trocar pelos tokens oficiais)

- Ouro (F / autoridade): `#D6A848` · hi `#F0CE84` · lo `#7E5E28`
- Violeta (H / pessoas): `#7C74E6` · hi `#A8A1F7` · lo `#4A44A6`
- Fundo: `#08080A` · superfícies `#15151B` / `#1C1C24`
