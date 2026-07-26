# DNS & E-mail — finhire.com.br (mapa verificado)

> Fonte: investigação read-only via Claude Chrome no Portal HostGator + cPanel
> em 2026-07 (nada foi alterado), conferida com consulta DNS externa.
> Este arquivo é o **backup do estado** e o **manual de segurança** antes de
> qualquer mudança de DNS/e-mail.

## Fatos verificados

- **Registro do domínio:** HostGator (registrado 22/06/2026, vence 22/05/2027,
  ciclo anual). Aparece no Portal do Cliente, **não vinculado a plano de
  hospedagem** ("Outra Plataforma de e-mail").
- **Zona DNS editada no PORTAL do cliente** (Domínios → Gerenciar → Configurar
  domínio → "Mostrar configuração manual da Zona de DNS"), **não no cPanel**.
  Nameservers `dns3/dns4.hostgator.com.br` ("protegido pela Cloudflare").
- **cPanel da hospedagem principal:** conta `vocemi24`, servidor `br996`,
  plano M, domínio primário `vocemilitarbrasil.com.br`, IP `162.241.203.70`
  (Portal exibe `162.241.203.67` como "Hostname FTP" — confirmar com o
  suporte antes de usar; a zona real do primário usa o `.70`).
- **Site:** GitHub Pages (apex nos 4 IPs 185.199.108–111.153). Deploy
  automático via push no GitHub — **motivo pelo qual o site NÃO deve migrar
  de hospedagem.**
- **E-mail:** ImprovMX (forwarding). Caixas reais não existem.
- **Transacional:** subdomínio `send.finhire.com.br` configurado para
  **Resend/Amazon SES** (SPF + DKIM + MX de feedback). Alguém envia e-mail
  transacional como @finhire.com.br por aí — **não apagar**.
- **App:** `app.finhire.com.br` → `185.158.133.1` (**Lovable**) + TXT de
  verificação `_lovable`. Existe um projeto Lovable vinculado — **não apagar**.

## Zona DNS completa (backup 2026-07 · TTL 14400 · classe IN)

| Tipo | Nome | Valor |
|---|---|---|
| A | finhire.com.br. | 185.199.108.153 |
| A | finhire.com.br. | 185.199.109.153 |
| A | finhire.com.br. | 185.199.110.153 |
| A | finhire.com.br. | 185.199.111.153 |
| CNAME | www.finhire.com.br. | finhire.com.br |
| CNAME | ftp.finhire.com.br. | finhire.com.br |
| CNAME | mail.finhire.com.br. | finhire.com.br |
| A | app.finhire.com.br. | 185.158.133.1 |
| TXT | _lovable.app.finhire.com.br. | lovable_verify=848e6b67… |
| MX 10 | finhire.com.br. | mx1.improvmx.com |
| MX 20 | finhire.com.br. | mx2.improvmx.com |
| TXT | finhire.com.br. | v=spf1 include:spf.improvmx.com ~all |
| TXT | _dmarc.finhire.com.br. | v=DMARC1; p=none; |
| TXT | send.finhire.com.br. | v=spf1 include:amazonses.com ~all |
| MX 10 | send.finhire.com.br. | feedback-smtp.sa-east-1.amazonses.com |
| TXT | resend._domainkey.finhire.com.br. | p=MIGfMA0GCSqG… (DKIM Resend) |

## ⛔ O botão proibido

**Portal → Configurar domínio → plataforma "HostGator" → Configurar.**
Esse assistente REESCREVE a zona automaticamente ("alterar DNS") e apontaria o
apex para o IP da hospedagem → **derruba o site do GitHub Pages e o e-mail**.
Ninguém da equipe toca nesse fluxo. O mesmo vale para os assistentes de
"plataforma de loja/site" do Portal.

O caminho seguro para adicionar o domínio à hospedagem é SEMPRE
**cPanel → Domínios → Create A New Domain** (não altera DNS público; cria
apenas vhost + pasta + zona local irrelevante no br996), com
**"Share document root" DESMARCADA**.

## Cenário 1 — domínio no cPanel, e-mail continua ImprovMX

- Ação: cPanel → Create A New Domain (`finhire.com.br`, document root próprio).
- Mudança de DNS público: **nenhuma** (zona do Portal fica idêntica).
- Ganho: domínio "aparece" na hospedagem; pré-requisito para caixas no futuro.
- Efeito colateral esperado: AutoSSL falha para esse domínio (inofensivo — o
  SSL do site é do GitHub Pages).

## Cenário 2 — caixas de e-mail reais na HostGator (equipe)

Pré-requisito: Cenário 1 feito. **MX é exclusivo: ativar caixas HostGator
desliga o ImprovMX** (os aliases atuais viram Encaminhadores no cPanel).

Mudanças na zona do Portal:

| Ação | Registro |
|---|---|
| Remover | MX 10 → mx1.improvmx.com |
| Remover | MX 20 → mx2.improvmx.com |
| Criar | MX 0 → mail.finhire.com.br |
| Alterar | TXT SPF do apex: `v=spf1 a mx include:websitewelcome.com ~all` |
| Substituir | CNAME `mail` → vira **A** `mail.finhire.com.br` → 162.241.203.70 (CNAME e A não coexistem) |
| Criar | A `webmail.finhire.com.br` → 162.241.203.70 |
| Provável | TXT `default._domainkey` (DKIM gerado pelo cPanel) |

**Intocáveis nos dois cenários:** 4× A do apex (GitHub Pages), CNAME `www`,
`app.finhire.com.br` + `_lovable` (Lovable), `_dmarc`, e todo o conjunto
`send.finhire.com.br` (Resend/SES).

### Ordem de execução recomendada (Cenário 2)

1. **Backup**: Portal → zona → "COPIAR REGISTROS DE DNS" → guardar o texto
   (colar neste arquivo, seção abaixo).
2. cPanel → Create A New Domain (share root DESMARCADO).
3. cPanel → Contas de E-mail → criar caixas (`empresas@`, `candidatos@`,
   `contato@`, pessoais da equipe) com senhas fortes.
4. cPanel → Encaminhadores → recriar o comportamento dos aliases que devem
   continuar caindo no Gmail de alguém (opcional).
5. cPanel → Distribuição de e-mail: **roteamento local** para o domínio.
6. Portal → zona DNS → aplicar a tabela acima (MX/SPF/mail/webmail).
7. Aguardar propagação (até ~4h pelo TTL 14400) e testar: enviar de fora →
   caixa; responder da caixa → Gmail externo; conferir spam/SPF nos headers.
8. Desativar/encerrar o domínio no painel ImprovMX só depois dos testes.

### Alternativas se a entregabilidade do IP compartilhado decepcionar

- Zoho Mail (grátis até 5 usuários) ou Google Workspace — mesma lógica de
  troca de MX, provedores com reputação melhor para envio em volume.

## Backup textual da zona (export "COPIAR REGISTROS DE DNS")

_(pendente — colar aqui quando capturado)_

## 📌 Handoff — e-mail marketing central (ADIADO, executar no hub)

Decisão de 2026-07 (Rodrigo): montar **Listmonk + Amazon SES** como
plataforma de e-mail marketing do GRUPO (todas as marcas), no projeto hub.
- Volume real: diário para 3–4k leads quentes + reativações da base de 15k
  → custo estimado ~R$ 115/mês (VPS ~R$ 35 + SES US$ 0,10/mil envios).
- Rodrigo possivelmente JÁ TEM uma VPS — verificar antes de contratar.
- Um subdomínio de envio por marca (`news.vocebancario.com.br`,
  `news.finhire.com.br`…) — nunca disparar das caixas corporativas.
- Falta decidir/fazer no hub: conta AWS própria (o SES visto no DNS é do
  Resend dos apps, não dele), pedido de saída do sandbox SES, instalação
  do Listmonk na VPS, DNS dos subdomínios de envio, plano de aquecimento.

## 🚨 Achado colateral (2026-07): SPF duplicado no vocebancario.com.br

Auditoria DNS do domínio principal revelou **DOIS registros SPF no apex**:

1. `v=spf1 a mx include:websitewelcome.com include:amazonses.com ~all`
2. `v=spf1 a mx include:websitewelcome.com ~all`  ← **redundante, apagar**

Pela RFC 7208, mais de um `v=spf1` no mesmo nome causa **PermError** — o
validador desiste e o e-mail perde a autenticação SPF (pior nota de spam
hoje, em todos os envios @vocebancario). Correção (2 min): na zona DNS do
vocebancario.com.br (cPanel → Zone Editor, ou Portal), **excluir o registro
nº 2** e manter só o nº 1 (que já inclui HostGator + Amazon SES).

Estado saudável verificado no mesmo domínio: MX local (mail.vocebancario),
DKIM cPanel presente (`default._domainkey`), DMARC `p=none`, e o IP da
hospedagem (162.241.203.70) **limpo** em Spamcop, Barracuda e SORBS.
