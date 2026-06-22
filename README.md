# FinHire — Landing Page

Landing page da **FinHire**, recrutamento e seleção especializado para o
**mercado financeiro** (vertical de carreiras do ecossistema @vocebancario —
futuro novo nome da VB Carreiras).

Mesma pegada de sofisticação da LP do Sales Trader: página única (HTML + CSS +
JS inline), tema escuro, acabamento metálico. O eixo cromático segue as logos
**FH** — **ouro** (autoridade/mercado) + **violeta** (pessoas/match).

## Estrutura

```
.
├── index.html              # página única (HTML + CSS + JS inline)
├── assets/
│   ├── favicon.svg         # monograma FH (placeholder até a arte final)
│   ├── README.md           # slots de arte a trocar (foto, OG, logos PNG)
│   ├── especialista.jpg    # (falta) foto do especialista — fallback "FH"
│   └── og.png              # (falta) preview social 1200×630
└── .github/workflows/pages.yml   # deploy automático no GitHub Pages
```

> ⚠️ **Identidade provisória, no feeling.** Cores, logo (desenhada em CSS) e
> alguns números são placeholders marcados com `[...]` no `index.html`. Trocar
> pelos tokens/arte oficiais quando chegarem.

## Conteúdo a finalizar (marcado com `[...]` no HTML)

- Número de WhatsApp do **Sandro** (hoje usa o comercial @vocebancario) —
  bloco `WA_PHONE` no `<script>` do `index.html`.
- Bio e números reais do especialista (Advisors no funil, instituições atendidas).
- Logos e depoimentos reais de instituições/profissionais (**não fabricar**).
- SLA médio de shortlist e praças prioritárias (FAQ).
- Foto `assets/especialista.jpg` e arte social `assets/og.png`.

## Publicação (GitHub Pages)

Deploy automático via GitHub Actions a cada push na branch publicada
(`main` ou a branch de desenvolvimento). A URL aparece em
**Settings → Pages** após o primeiro deploy. Para domínio próprio, adicionar
um arquivo `CNAME` na raiz com o domínio (ex.: `finhire.com.br`).
