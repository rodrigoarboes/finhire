# Prompt de verificação final — e-mail finhire.com.br (sessão 3)

> Migração concluída nas sessões 1 e 2 (caixas, encaminhadores, MX, SPF com
> ip4, DKIM — tudo confirmado externamente via DNS). Esta sessão é de
> AUDITORIA: conferir e reportar, sem alterar nada.
> Colar no Claude in Chrome com Portal HostGator + cPanel logados.

```
MISSÃO: AUDITORIA FINAL da configuração de e-mail do finhire.com.br.
Esta missão é SOMENTE LEITURA: você confere e reporta. Se encontrar
qualquer coisa divergente, NÃO corrija — anote no relatório e me mostre.
A única exceção com ação é a Etapa 5 (teste do mail-tester), onde EU digito
o login. Me explique cada passo em 1 linha.

CONTEXTO: migração já concluída em sessões anteriores. E-mail do
finhire.com.br agora é caixas reais no cPanel (conta vocemi24, servidor
br996). Site no GitHub Pages — intocável. Encaminhamentos já estão
entregando na prática.

ETAPA 1 — CAIXAS (cPanel → E-mail → Contas de E-mail, filtrar "finhire")
Conferir que existem exatamente estas 7 caixas, todas com quota 2048 MB:
empresas@ · candidatos@ · contato@ · financeiro@ · sandro.rodrigues@ ·
silvia.rodrigues@ · rodrigo.arboes@  (todas @finhire.com.br)

ETAPA 2 — ENCAMINHADORES (cPanel → E-mail → Encaminhadores, domínio finhire)
Conferir que existem exatamente estes 15:
- empresas@   → rarboesclaude@gmail.com, rodrigo.arboes@vocebancario.com.br,
                sandrorrv@gmail.com
- candidatos@ → os mesmos 3 destinos
- contato@    → os mesmos 3 destinos
- financeiro@ → financeiro@vocebancario.com.br, rarboesclaude@gmail.com
- sandro.rodrigues@  → sandrorrv@gmail.com
- silvia.rodrigues@  → sandrorrv@gmail.com
- rodrigo.arboes@    → rodrigo.arboes@vocebancario.com.br,
                       rarboesclaude@gmail.com
Faltando ou sobrando algum, só anotar.

ETAPA 3 — AUTENTICAÇÃO (cPanel → E-mail → Capacidade de Entrega de E-mail)
Linha finhire.com.br: deve mostrar SPF VÁLIDO e DKIM VÁLIDO.
Se a tela sugerir qualquer alteração adicional, NÃO aplicar — copiar a
sugestão para o relatório. Conferir também que o Email Routing
(Distribuição de E-mail) do finhire.com.br está em "Local Mail Exchanger".

ETAPA 4 — ZONA DNS (Portal → Domínios → finhire.com.br → Configurar →
configuração manual da zona; SOMENTE LEITURA)
A zona deve conter exatamente:
- 4× A apex: 185.199.108.153 / 109.153 / 110.153 / 111.153 (site GitHub)
- CNAME www → finhire.com.br  ·  CNAME ftp → finhire.com.br
- A mail → 162.241.203.70  ·  A webmail → 162.241.203.70
- MX 0 → mail.finhire.com.br
- TXT apex: "v=spf1 a mx ip4:162.241.203.67 include:websitewelcome.com ~all"
  (deve ser o ÚNICO v=spf1 do apex)
- TXT default._domainkey → v=DKIM1... (DKIM)
- A app → 185.158.133.1  ·  TXT _lovable.app  ·  TXT _dmarc
- TXT + MX de send.finhire.com.br (Amazon SES)  ·  TXT resend._domainkey
NÃO deve existir: nenhum registro com "improvmx".
Divergiu? Print + anotar, sem tocar.

ETAPA 5 — NOTA DE ENTREGABILIDADE (única com ação; eu participo)
1. Abra mail-tester.com e copie o endereço de teste exibido.
2. Abra webmail.finhire.com.br (ou cPanel → Contas de E-mail → empresas@ →
   Check Email) e PAUSE — eu faço o login da caixa empresas@.
3. Com a caixa aberta, me guie: enviar um e-mail para o endereço do
   mail-tester com assunto "Apresentação FinHire" e 2 frases de texto normal.
4. Volte ao mail-tester, clique em ver resultado e anote a NOTA e os
   principais apontamentos (SPF, DKIM, blacklists).

ETAPA 6 — RELATÓRIO FINAL
Entregar: resultado das etapas 1–4 (ok/divergências), a nota do mail-tester
com os apontamentos, e qualquer sugestão pendente do cPanel. Sem senhas.
```
