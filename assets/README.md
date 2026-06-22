# assets — FinHire

Arte da marca usada na landing page. **A logo no site hoje é desenhada em CSS**
(monograma FH + wordmark FinHire), então a página já sobe bonita sem depender
de imagem. Os arquivos abaixo são os "slots" pra quando a identidade final chegar.

## O que trocar quando tiver a arte oficial

| Arquivo | Onde aparece | Status |
|---|---|---|
| `favicon.svg` | Aba do navegador | ✅ placeholder (monograma FH) — trocar pelo ícone final |
| `especialista.jpg` | Bloco "Quem conduz a sua contratação" | ⬜ falta — cai em fallback "FH" se ausente |
| `og.png` | Preview ao compartilhar o link (1200×630) | ⬜ falta — recomendado pra WhatsApp/redes |
| `logo-dark.png` / `logo-light.png` / `logo-mono.png` | (opcional) substituir a logo CSS por PNG | ⬜ opcional |

> A logo CSS replica a pegada das logos FH (F ouro + H violeta, "Fin" branco +
> "Hire" violeta). Quando você mandar os PNGs definitivos, dá pra trocar o
> bloco `.brand` por `<img>` em 2 linhas — me avisa que eu faço.

## Paleta provisória (no feeling — trocar pelos tokens oficiais)

- Ouro (F / autoridade): `#D6A848` · hi `#F0CE84` · lo `#7E5E28`
- Violeta (H / pessoas): `#7C74E6` · hi `#A8A1F7` · lo `#4A44A6`
- Fundo: `#08080A` · superfícies `#15151B` / `#1C1C24`
