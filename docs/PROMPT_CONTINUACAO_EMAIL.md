# Prompt de retomada — migração de e-mail finhire.com.br (sessão 2)

> A sessão anterior do Claude in Chrome caiu durante a Fase 6 (DKIM).
> Estado abaixo foi verificado externamente via DNS em seguida.
> Colar o bloco no Claude in Chrome com Portal HostGator + cPanel logados.

```
MISSÃO: RETOMAR uma migração de e-mail que foi interrompida no meio (a sessão
anterior caiu). Quase tudo já foi feito e VERIFICADO por fora — não refaça
nada da lista "JÁ FEITO". Execute apenas as etapas de "FALTA FAZER", na ordem.
Me explique cada passo em 1 linha.

CONTEXTO:
- Domínio finhire.com.br. Site no GitHub Pages (não sai de lá). Caixas de
  e-mail novas no cPanel da HostGator (conta vocemi24, servidor br996).
- A zona DNS do finhire.com.br é editada no PORTAL do cliente
  (Domínios → Gerenciar → Configurar domínio → configuração manual da zona).
  A zona do vocebancario.com.br fica no cPanel → Zone Editor.

REGRAS DE SEGURANÇA:
1. NUNCA usar o assistente do Portal "Configurar domínio → plataforma
   HostGator/loja/site" — ele reescreve o DNS e derruba o site.
2. Na zona do finhire.com.br NUNCA tocar em: 4× A do apex
   (185.199.108/109/110/111.153), CNAME www, CNAME ftp, A app.finhire.com.br
   (185.158.133.1), TXT _lovable.app, TXT _dmarc, e tudo de
   send.finhire.com.br + resend._domainkey (SES/Resend).
3. Se qualquer tela divergir do descrito, PARE e me mostre.
4. Senhas: você NÃO gera, NÃO lê e NÃO anota senha nenhuma. Onde precisar de
   senha, abra a tela e PAUSE para eu digitar.

JÁ FEITO (não refazer; verificado externamente via DNS):
- SPF duplicado do vocebancario.com.br corrigido (restou um único v=spf1).
- finhire.com.br adicionado ao cPanel (root próprio, share desmarcado).
- 4 caixas criadas: empresas@, candidatos@, contato@, sandro@ (2 GB cada).
  Senhas NÃO foram retidas — serão definidas pelo Rodrigo na Etapa 2.
- Email Routing do finhire.com.br fixado em "Local Mail Exchanger".
- Zona DNS do finhire.com.br JÁ ALTERADA e no ar: MX 0 → mail.finhire.com.br;
  A mail → 162.241.203.70; A webmail → 162.241.203.70; SPF do apex agora é
  "v=spf1 a mx include:websitewelcome.com ~all"; os 2 MX do ImprovMX e o
  CNAME mail foram removidos. Site intacto.

FALTA FAZER:

ETAPA 0 — CONFERÊNCIA RÁPIDA (read-only)
Abra a zona do finhire.com.br no Portal e confira que ela contém exatamente:
4× A apex (185.199.108–111.153) · CNAME www · CNAME ftp · A mail →
162.241.203.70 · A webmail → 162.241.203.70 · MX 0 → mail.finhire.com.br ·
TXT apex "v=spf1 a mx include:websitewelcome.com ~all" · A app →
185.158.133.1 · TXT _lovable.app · TXT _dmarc · TXT + MX de
send.finhire.com.br (SES) · TXT resend._domainkey.
NÃO deve haver: MX improvmx, CNAME mail, TXT com spf.improvmx.com.
Se bater, siga. Se divergir, pare e me mostre.

ETAPA 1 — DKIM (a pendência que ficou)
1. cPanel → E-mail → Capacidade de Entrega de E-mail (Email Deliverability)
   → linha finhire.com.br → Gerenciar.
2. No bloco DKIM (default._domainkey), use o botão COPIAR do valor sugerido.
3. Portal → zona do finhire.com.br → ADICIONAR registro TXT:
   Nome: default._domainkey   (autocompleta p/ default._domainkey.finhire.com.br.)
   Valor: colar o que copiou (v=DKIM1; k=rsa; p=...)
   Salvar.
4. Volte à tela de Capacidade de Entrega e recarregue — pode levar alguns
   minutos até validar. Se seguir "inválido" após ~15 min, me mostre.

ETAPA 2 — SENHAS (pausa para o Rodrigo, caixa por caixa)
cPanel → E-mail → Contas de E-mail → filtrar "finhire":
para CADA caixa (empresas@, candidatos@, contato@, sandro@):
Gerenciar → campo Nova senha → PAUSE e deixe o Rodrigo digitar a senha que
ele escolher no gerenciador dele → Salvar → próxima.

ETAPA 3 — ENCAMINHADORES (cópia para o Gmail)
ANTES de criar, me pergunte UMA vez: "cópias para qual Gmail —
(A) rodrigoarboes@gmail.com ou (B) rarboesclaude@gmail.com?"
(Os 8 encaminhadores existentes da conta apontam para o B; a instrução
original dizia A. O Rodrigo decide.)
Depois: cPanel → E-mail → Encaminhadores → Adicionar encaminhador, domínio
finhire.com.br, para: empresas@, candidatos@ e contato@ → destino escolhido.
(sandro@ fica SEM cópia.)

ETAPA 4 — TESTES (o DNS novo já propagou; pode testar direto)
1. De um Gmail externo, envie para empresas@finhire.com.br. Confira:
   chegou no webmail (cPanel → Contas de E-mail → Check Email) E a cópia
   chegou no Gmail escolhido na Etapa 3?
2. Responda do webmail para o Gmail. Chegou na caixa de ENTRADA (não spam)?
   Em "Mostrar original" no Gmail: SPF=PASS e DKIM=PASS?
3. Abra mail-tester.com, copie o endereço de teste, envie um e-mail da caixa
   empresas@ para ele e anote a NOTA (esperado 9–10 com DKIM ok).

ETAPA 5 — RELATÓRIO FINAL (sem senhas!)
Incluir: confirmação da Etapa 0 (zona conferida), DKIM criado e validado,
senhas redefinidas (só "feito", sem valores), encaminhadores criados e para
qual destino, resultado dos 3 testes com a nota do mail-tester, e qualquer
divergência.
```
