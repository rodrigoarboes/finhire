# FinHire — Landing Page

Landing page da **FinHire**, recrutamento e seleção especializado para o
**mercado financeiro** (marca de carreiras do grupo Você Bancário — evolução
da VB Carreiras).

Página única (HTML + CSS + JS inline), tema escuro, acabamento metálico, na
mesma pegada de sofisticação da LP do Sales Trader. Eixo cromático seguindo as
logos **FH** — **ouro** (autoridade/mercado) + **violeta** (pessoas/match).

## Estrutura

```
.
├── index.html              # página única (HTML + CSS + JS inline)
├── CNAME                   # domínio custom: finhire.com.br
├── assets/
│   ├── favicon.svg         # monograma FH (placeholder até a arte final)
│   ├── README.md           # slots de arte a subir (fotos, OG, logos)
│   ├── sandro.jpg          # (subir) foto do Sandro — fallback "SV"
│   ├── rodrigo.jpg         # (subir) foto do Rodrigo — fallback "RA"
│   └── og.png              # (subir) preview social 1200×630
└── .github/workflows/pages.yml   # deploy automático no GitHub Pages
```

## Seções

Nav sticky · hero · faixa de stats (66.500+ / 10.000+ / 30+ / 5min) · dor ·
soluções (R&S, Pré-Qualificação por vídeo, Treinamento, Divulgação) · processo
(5 passos) · quem somos (Sandro + Rodrigo) · instituições · para candidatos ·
contato · FAQ · CTA final · footer.

## Conteúdo a finalizar (marcado com `[...]` no HTML)

- **Fotos**: subir `assets/sandro.jpg` (terno) e `assets/rodrigo.jpg` (polo) —
  ver `assets/README.md`.
- **WhatsApp**: hoje usa `(11) 98822-2442` (contato VB Carreiras). Confirmar se
  é o número oficial da FinHire — bloco `WA_PHONE` no `<script>`.
- **E-mail / CNPJ**: `contato@vbcarreiras.com.br` e CNPJ `63.117.156/0001-77` —
  confirmar se troca para domínio/razão social FinHire.
- **SLA** de shortlist (FAQ) e arte social `assets/og.png`.

## Domínio (finhire.com.br)

O arquivo `CNAME` já aponta para `finhire.com.br`. Falta configurar o **DNS**
no registrador do domínio (registros A do GitHub Pages para o apex + CNAME do
`www`). Enquanto o DNS não propaga, o site fica acessível em
`https://rodrigoarboes.github.io/finhire/`.

## Publicação (GitHub Pages)

Deploy automático via GitHub Actions a cada push na branch publicada
(`main` ou a branch de desenvolvimento). Source: **GitHub Actions** (já ligado).
