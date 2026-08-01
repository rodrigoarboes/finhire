# Estudo de concorrência — InHire (ATS usado pela EQI)

> Levantamento feito pelo Rodrigo via Claude in Chrome em 2026-07, sobre
> `carreira.inhire.com.br/carreiras/eqi`, os 3 portais `eqi.inhire.app`
> (assessoria, apoio, PCD) e uma vaga aberta com formulário.
> Abaixo: o estudo na íntegra + triagem de ação da FinHire/VB.

## TRIAGEM — o que fazer com isso

### ✅ Já temos (e eles não)
- **A escada N1–N5** (site + deck) é exatamente o "campo estruturado de
  certificação/senioridade" que falta no InHire — a bifurcação
  formação × experiente que o estudo aponta como roadmap vertical.
- **Ecossistema de formação próprio** (Academia, MAP, mentorias): o
  "ATS↔LMS" que o estudo sugere já existe como operação — falta virar
  software (vbcarreiras/app FinHire).
- **Links rastreados de indicação**: os stubs `wvagas-ind-rc`,
  `wvagas-ind-rca`, `wvagas-ind-membro` etc. já são rastreamento de
  indicação por canal — o que o InHire não oferece.
- **Site estático server-rendered por natureza** (GitHub Pages): a fraqueza
  técnica deles (client-side sem SEO) não nos afeta.

### ⚡ Quick wins aplicáveis agora (site/funil FinHire)
1. **Etapas do processo visíveis ao candidato** no fim do funil `/vagas/`
   (Cadastro → conversa → parecer em 24h → apresentação ao cliente) —
   reduz ansiedade, custa 10 linhas de HTML.
2. **Roteiro de onboarding mês a mês** como template de descrição de vaga
   para clientes (1º mês imersão → 4º mês carteira) — vira material do
   playbook comercial/pareceres.

### 🏗️ Roadmap de produto (vbcarreiras / app.finhire — executar no hub)
- Certificação como campo estruturado (tipo, número, validade) +
  verificação automática Anbima/Ancord.
- Bifurcação automática do pipeline por status de certificação (trilha
  formação × experiente) — espelhando a régua N1–N5.
- Progresso no LMS como score de ranqueamento do candidato.
- Campo confidencial de book/carteira sob gestão (KPI real de contratação
  de assessor experiente).
- Multiunidade/white-label: portais por praça/escritório B2B com domínio
  do cliente (`carreira.cliente.com.br`) — SEO acumula no cliente, não no
  fornecedor (fraqueza comercial do InHire).
- Páginas de vaga SSR + schema JobPosting + Google for Jobs/LinkedIn/
  Indeed/Catho — vantagem mensurável em volume de candidatos.
- Portais segmentados por público (assessoria/apoio/PCD) + acessibilidade
  (Libras) + multi-idioma: recursos deles que valem replicar.
- Área do candidato com status da candidatura + alertas de vaga + banco de
  talentos com opt-in (o portal do candidato do vbcarreiras já é o embrião).

### 💼 Munição comercial (deck/pitch futuro)
- "ATS genérico não resolve o nicho" — o caso EQI×InHire prova a tese da
  FinHire; usar quando o pitch evoluir para produto.
- White-label de domínio próprio como diferencial fácil de vender.

---

## ESTUDO NA ÍNTEGRA (Claude in Chrome, 2026-07)

### Como a InHire estrutura o produto

A arquitetura é de duas camadas. Existe uma página institucional de
employer branding hospedada no domínio da própria InHire, bem rica em
conteúdo (sobre nós, "nossos números", diferenciais, carrossel de valores,
benefícios, CTAs), e separada dela ficam os portais de vagas num subdomínio
do cliente dentro do `inhire.app`. Quem candidata sai de um domínio e cai
em outro.

O ponto mais interessante do produto é a **segmentação em múltiplos portais
por tenant**: a EQI tem um hub para assessoria de investimentos, outro para
áreas de apoio e outro para PCD, cada um com hero, texto institucional e
pool de vagas próprios. Jornadas de candidato distintas por público-alvo,
com narrativa sob medida. Complementando, seletor de idiomas em quatro
variantes (EN, PT-PT, PT-BR, ES) e plugin de acessibilidade em Libras
(Hand Talk), além do portal PCD dedicado.

Na página da vaga, dois detalhes bem feitos: as **etapas do processo ficam
visíveis ao candidato** (Cadastro → "Queremos conhecer você" → bate-papo
com o gestor → proposta → contratação) e o **formulário é inline, sem
criação de conta**. Fricção baixíssima: nome, CPF (toggle "não sou
brasileiro" abre país de origem), e-mail, celular, cidade, pergunta
eliminatória configurável, upload de currículo e pretensão salarial
rotulada "como CLT" (campo sensível ao tipo de contrato — relevante num
setor com muito PJ). Política de privacidade no rodapé do form,
consentimento implícito no envio.

### Fraquezas que são oportunidade direta para a FinHire

A mais gritante é técnica: portais renderizados no client-side — conteúdo
só existe depois do JS — sem dados estruturados de vaga. Indexação ruim no
Google e provável ausência no Google for Jobs. Páginas de vaga SSR com
schema JobPosting e distribuição automática (Google Jobs, LinkedIn, Indeed,
Catho) entram com vantagem mensurável em volume de candidatos — a métrica
que o cliente sente.

O domínio de carreiras é da InHire, não do cliente (SEO acumula no
fornecedor), e o rodapé carrega "© InHire". Domínio próprio white-label
(`carreira.cliente.com.br`) é diferencial comercial fácil de vender.

Filtros pobres — só nome da vaga, modelo de atuação e localização. Falta
área/departamento, senioridade, tipo de contrato, tags. Não há alertas de
vagas, banco de talentos com opt-in, vagas similares, favoritar, nem área
do candidato para acompanhar status. Botão de compartilhar existe, mas nada
de programa de indicação com link rastreado — e em assessoria de
investimentos indicação é o canal principal de contratação.

### O insight vertical

O caso EQI mostra que recrutamento em assessoria de investimentos é
problema de nicho que ATS genérico não resolve bem. O funil deles: alto
volume, 14 escritórios próprios + 50+ escritórios B2B, barreira de
certificação (CPA-20, CEA, CFP, Ancord) e — o mais revelador — **o programa
de certificação gratuito é a isca de recrutamento**, com 1.000+ aprovados e
EaD própria com 350+ treinamentos.

Roadmap vertical defensável: certificação como campo estruturado com
verificação automática Anbima/Ancord; bifurcação do pipeline
formação × experiente; ATS↔LMS (progresso no curso vira score);
campo estruturado e confidencial de book/carteira sob gestão; gestão
multiunidade para franquias/B2B sob marca-mãe com governança central;
integrações nativas com CRM (EQI usa Salesforce) e folha/HRIS.

### Conteúdo e templates para copiar

Blocos prontos que valem replicar: "nossos números" com contadores
animados; carrossel de valores; lista de benefícios; e principalmente o
**roteiro de onboarding mês a mês na descrição da vaga** (1º mês imersão,
2º afinamento comercial, 3º–4º captação e estruturação de carteira, com
entrega de base de clientes ao final) — reduz a ansiedade do candidato
comercial. Gerador de descrição de vagas com linguagem do mercado
financeiro e cuidado com compliance fecha o pacote.
