# FinHire — Site (institucional + funil de candidato)

Repositório do **finhire.com.br** (HTML/CSS/JS estático, deploy no GitHub Pages).
Dois públicos, duas portas — medição unificada por GTM.

## Rotas

| URL | O que é |
|---|---|
| `finhire.com.br` (`index.html`) | **Site institucional B2B** — Talent Solutions (copy final) |
| `finhire.com.br/vagas/` | **Funil de candidato** — quiz (estado/cidade/experiência/disponibilidade) |
| `finhire.com.br/wvagas-*` | ~27 **links de rastreio** por canal → `/vagas/?c=<canal>` (IG/FB/Telegram/TikTok/LinkedIn/mail…) |
| `finhire.com.br/deck.html` | **Deck público** — 11 slides A4 paisagem (sem histórico C6) |
| `/deck-completo.html` (não linkado) | **Deck completo** — 12 slides, com histórico C6 (enviar só ao C6) |

## Medição
**Google Tag Manager `GTM-WM593476`** em todas as páginas — inclusive no institucional (enxertado na reconciliação).

## Identidade
Violeta primário `#6354E8` · dourado champagne `#C9A24C` · dark mode · **Inter** ·
assets reais em `assets/` (logos + fotos dos fundadores).

## Contatos (institucional)
- **Empresas (B2B):** `empresas@finhire.com.br` + WhatsApp institucional
- **Profissionais:** `candidatos@finhire.com.br` (e o funil em `/vagas/`)
- LinkedIn: `linkedin.com/showcase/finhirebr`

## E-mail (infra) — ✅ MIGRADO para caixas HostGator (2026-07, auditado 10/10)
> História completa, zona DNS final, mapa de encaminhadores e runbooks:
> **docs/DNS_EMAIL_FINHIRE.md**
- **Caixas reais no cPanel** (conta `vocemi24`, servidor br996), 2 GB cada:
  `empresas@`, `candidatos@`, `contato@`, `financeiro@`, `sandro.rodrigues@`,
  `silvia.rodrigues@`, `rodrigo.arboes@`. Webmail: `webmail.finhire.com.br`.
- **Encaminhadores (15):** institucionais copiam p/ `rodrigo.arboes@vocebancario.com.br`,
  `sandrorrv@gmail.com` (Sandro) e `rarboesclaude@gmail.com` (caixa do assistente
  de IA do Rodrigo); pessoais copiam pro dono. Caixa sempre retém o original.
- **Autenticação:** SPF `v=spf1 a mx ip4:162.241.203.67 include:websitewelcome.com ~all`,
  DKIM `default._domainkey` e PTR — todos VÁLIDOS; mail-tester **10/10**, sem blacklists.
- **DNS:** a zona autoritativa é editada no **Portal** HostGator (existe uma
  zona local órfã no cPanel que **não vale** — ignorar). Site segue no GitHub Pages.
- **ImprovMX:** desligado de fato (MX removido). Encerrar a conta lá é limpeza
  opcional após ~1 semana de observação.

## Deck → PDF
Abrir `deck.html` no Chrome → **Ctrl/Cmd+P** → *Salvar como PDF* · Layout **Paisagem** ·
Margens **Nenhuma** · marcar **Gráficos de plano de fundo** · Escala 100%.

## Pendências (dependem do Rodrigo)
- ✅ **E-mail resolvido (2026-07):** caixas HostGator no ar com nota 10/10 — ver `docs/DNS_EMAIL_FINHIRE.md`. Resta só limpeza opcional (encerrar conta ImprovMX após ~1 semana).
- Exportar o PDF do deck (Ctrl+P) — ambiente sem renderizador headless.
- Confirmar LinkedIn showcase `finhirebr` no ar.

## Regras de conteúdo (institucional — respeitadas)
Cliente âncora sempre anônimo ("uma grande corretora de valores"); histórico C6 só no
deck (slide 5); sem "90% de aprovação"; sem BTG na bio do Rodrigo; sem Zanella Wealth;
números do grupo: desde 2017 · +20 mil impactados · +75 mil audiência.
