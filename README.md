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

## E-mail (infra) — verificado em 2026-07 via DNS
> Mapa completo da zona DNS, o "botão proibido" do Portal e o roteiro de
> migração para caixas HostGator: **docs/DNS_EMAIL_FINHIRE.md**
- **DNS do domínio:** HostGator (nameservers `dns3/dns4.hostgator.com.br`) — a zona é editada no painel da HostGator.
- **E-mail:** **ImprovMX** (redirecionamento/forwarding) — MX `mx1/mx2.improvmx.com`, SPF `spf.improvmx.com`. **Não são caixas HostGator.**
- **Criar/gerenciar endereços:** `app.improvmx.com` → domínio `finhire.com.br` → *Aliases*. Alias novo entra na hora, grátis; um alias pode ter **vários destinos** (ex.: `candidatos@` → Gmail do Rodrigo + do Sandro). Se houver alias catch-all (`*`), qualquer endereço @finhire.com.br já encaminha.
- **Limitação:** forwarding só **recebe**. Para a equipe **responder como** @finhire.com.br é preciso SMTP do ImprovMX (plano pago) ou migrar os MX para caixas reais (Zoho Mail tem plano grátis p/ até 5 usuários; Google Workspace é o padrão profissional). A troca de MX se faz no painel da HostGator.

## Deck → PDF
Abrir `deck.html` no Chrome → **Ctrl/Cmd+P** → *Salvar como PDF* · Layout **Paisagem** ·
Margens **Nenhuma** · marcar **Gráficos de plano de fundo** · Escala 100%.

## Pendências (dependem do Rodrigo)
- Conferir no ImprovMX os aliases `empresas@`, `candidatos@` e `contato@` (se não houver catch-all `*`, criar — contato@ vai no slide final do deck).
- Exportar o PDF do deck (Ctrl+P) — ambiente sem renderizador headless.
- Confirmar LinkedIn showcase `finhirebr` no ar.

## Regras de conteúdo (institucional — respeitadas)
Cliente âncora sempre anônimo ("uma grande corretora de valores"); histórico C6 só no
deck (slide 5); sem "90% de aprovação"; sem BTG na bio do Rodrigo; sem Zanella Wealth;
números do grupo: desde 2017 · +20 mil impactados · +75 mil audiência.
