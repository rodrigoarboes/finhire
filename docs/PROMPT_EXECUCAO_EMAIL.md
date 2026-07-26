# Prompt de execução — e-mails FinHire + fix SPF VB (Claude in Chrome)

> Colar no Claude in Chrome com o Rodrigo logado no Portal HostGator e no cPanel.
> Gerado a partir de docs/DNS_EMAIL_FINHIRE.md em 2026-07.

```
MISSÃO: colocar os e-mails do finhire.com.br para funcionar com caixas reais
na HostGator e corrigir um bug de SPF no vocebancario.com.br. EXECUTAR na
ordem exata das fases. Sou leigo em DNS — me explique o que está fazendo em
1 linha por passo.

CONTEXTO:
- O site finhire.com.br fica no GitHub Pages e NÃO sai de lá.
- O e-mail do finhire hoje é redirecionamento via ImprovMX; vamos migrar para
  caixas reais no cPanel (conta vocemi24, servidor br996, plano M).
- A zona DNS do finhire.com.br é editada no PORTAL do cliente (não no cPanel).

REGRAS DE SEGURANÇA (valem a missão inteira):
1. NUNCA usar o assistente do Portal "Configurar domínio → plataforma
   HostGator/loja/site" — ele reescreve o DNS e derruba o site. Toda edição
   de DNS é MANUAL, registro por registro.
2. Na zona do finhire.com.br, NUNCA tocar em: os 4 registros A do apex
   (185.199.108/109/110/111.153), o CNAME www, o A de app.finhire.com.br
   (185.158.133.1), o TXT _lovable.app, o TXT _dmarc, e TUDO que envolva
   send.finhire.com.br e resend._domainkey (MX/TXT do Amazon SES/Resend).
3. Se qualquer tela divergir do descrito, PARE e me mostre antes de seguir.
4. Senhas de caixas: use o gerador do cPanel e PAUSE para eu anotar cada uma
   no meu gerenciador antes de continuar. NÃO incluir senhas no relatório.

FASE 0 — BACKUP (obrigatória; sem isso não prossiga)
1. Portal → Domínios → finhire.com.br → Configurar domínio → zona DNS →
   botão "COPIAR REGISTROS DE DNS". Guarde o texto integral para o relatório.

FASE 1 — FIX SPF DO VOCEBANCARIO.COM.BR (independente, 2 min)
1. Localize a zona do vocebancario.com.br (tente cPanel → Zone Editor;
   se não estiver, Portal → Domínios).
2. O apex tem DOIS registros TXT "v=spf1". EXCLUA APENAS este:
   v=spf1 a mx include:websitewelcome.com ~all   (o SEM amazonses)
3. MANTENHA: v=spf1 a mx include:websitewelcome.com include:amazonses.com ~all
   Não toque em mais nada (nem no google-site-verification).
4. Confirme que restou exatamente UM "v=spf1" no apex.

FASE 2 — ADICIONAR O DOMÍNIO AO CPANEL
1. cPanel → Domínios → Create A New Domain → finhire.com.br.
2. "Share document root": DESMARCADA. Diretório sugerido ok. Enviar.
3. (AutoSSL pode reclamar depois desse domínio — ignorar, o SSL do site é
   do GitHub Pages.)

FASE 3 — CRIAR AS CAIXAS
cPanel → E-mail → Contas de E-mail → Criar (domínio finhire.com.br):
- empresas@finhire.com.br
- candidatos@finhire.com.br
- contato@finhire.com.br
- sandro@finhire.com.br (me pergunte na hora se crio agora)
Senha pelo gerador (pausando p/ eu anotar), espaço 2048 MB ou ilimitado.

FASE 4 — CÓPIA PARA O GMAIL + ROTEAMENTO
1. cPanel → E-mail → Encaminhadores → Adicionar: para empresas@, candidatos@
   e contato@, encaminhar para rodrigoarboes@gmail.com. (Com caixa +
   encaminhador, o cPanel entrega na caixa E manda cópia — continuo vendo
   tudo no Gmail como hoje.)
2. cPanel → E-mail → Distribuição de E-mail (Email Routing) →
   finhire.com.br → "Local Mail Exchanger".

FASE 5 — TROCAR O DNS (zona do Portal, edição manual)
Antes: no cPanel Zone Editor, veja o IP do registro A de
mail.vocemilitarbrasil.com.br (domínio primário). Esperado: 162.241.203.70.
Use o IP que encontrar ("[IP]") e registre no relatório.
Na zona do finhire.com.br:
1. EXCLUIR: MX 10 → mx1.improvmx.com  e  MX 20 → mx2.improvmx.com
2. CRIAR:   MX prioridade 0 → mail.finhire.com.br
3. EXCLUIR o CNAME mail.finhire.com.br → finhire.com.br e CRIAR no lugar:
   A  mail.finhire.com.br → [IP]
4. CRIAR:   A  webmail.finhire.com.br → [IP]
5. ALTERAR o TXT do apex de "v=spf1 include:spf.improvmx.com ~all" para:
   v=spf1 a mx include:websitewelcome.com ~all
6. Mais NADA (regras de segurança).

FASE 6 — DKIM
1. cPanel → E-mail → Capacidade de Entrega (Email Deliverability) →
   finhire.com.br → copie o valor do DKIM sugerido (default._domainkey).
2. Na zona do Portal, CRIAR TXT default._domainkey.finhire.com.br com esse
   valor exato. (Se a tela sugerir outro SPF, ignore — já definimos o nosso.)

FASE 7 — TESTES (após propagação; TTL 4h, pode ser antes)
1. De um Gmail externo → enviar para empresas@finhire.com.br → conferir no
   webmail (cPanel → Contas de E-mail → Check Email) E a cópia no meu Gmail.
2. Responder do webmail para o Gmail → chegou na entrada (não spam)? Nos
   detalhes da mensagem: SPF=pass e DKIM=pass?
3. Enviar da caixa para o endereço gerado em mail-tester.com → anotar a nota.
4. ImprovMX: NÃO mexer hoje. Com o MX trocado ele fica inativo sozinho;
   remover a conta lá é limpeza opcional para daqui a 1 semana.

FASE 8 — RELATÓRIO FINAL
Incluir: texto integral do backup (Fase 0); confirmação do SPF único no
vocebancario; print da zona final do finhire; IP usado; caixas criadas (SEM
senhas); encaminhadores; resultado dos 3 testes + nota do mail-tester;
divergências encontradas.
```
