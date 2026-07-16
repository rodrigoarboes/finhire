# FinHire — Site (institucional + funil de candidato)

Repositório do **finhire.com.br** (HTML/CSS/JS estático, deploy no GitHub Pages).
Dois públicos, duas portas — medição unificada por GTM.

## Rotas

| URL | O que é |
|---|---|
| `finhire.com.br` (`index.html`) | **Site institucional B2B** — Talent Solutions (copy final) |
| `finhire.com.br/vagas/` | **Funil de candidato** — quiz (estado/cidade/experiência/disponibilidade) |
| `finhire.com.br/wvagas-*` | ~27 **links de rastreio** por canal → `/vagas/?c=<canal>` (IG/FB/Telegram/TikTok/LinkedIn/mail…) |
| `finhire.com.br/deck.html` | **Deck** 11 slides (16:9) para exportar em PDF (C6) |

## Medição
**Google Tag Manager `GTM-WM593476`** em todas as páginas — inclusive no institucional (enxertado na reconciliação).

## Identidade
Violeta primário `#6354E8` · dourado champagne `#C9A24C` · dark mode · **Inter** ·
assets reais em `assets/` (logos + fotos dos fundadores).

## Contatos (institucional)
- **Empresas (B2B):** `empresas@finhire.com.br` + WhatsApp institucional
- **Profissionais:** `candidatos@finhire.com.br` (e o funil em `/vagas/`)
- LinkedIn: `linkedin.com/showcase/finhirebr`

## Deck → PDF
Abrir `deck.html` no Chrome → **Ctrl/Cmd+P** → *Salvar como PDF* · Layout **Paisagem** ·
Margens **Nenhuma** · marcar **Gráficos de plano de fundo** · Escala 100%.

## Pendências (dependem do Rodrigo)
- Criar caixas `empresas@`, `candidatos@` e `contato@finhire.com.br` (contato@ vai no slide 11 do deck).
- Exportar o PDF do deck (Ctrl+P) — ambiente sem renderizador headless.
- Confirmar LinkedIn showcase `finhirebr` no ar.

## Regras de conteúdo (institucional — respeitadas)
Cliente âncora sempre anônimo ("uma grande corretora de valores"); histórico C6 só no
deck (slide 5); sem "90% de aprovação"; sem BTG na bio do Rodrigo; sem Zanella Wealth;
números do grupo: desde 2017 · +20 mil impactados · +75 mil audiência.
