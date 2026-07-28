# Projeto: Plano de Aprovação PRF — Documentação para retomada

> Este arquivo existe para que qualquer IA (ou você mesmo) consiga entender, adaptar ou
> melhorar o sistema sem precisar do histórico do chat original. Cole este arquivo inteiro
> no início de uma nova conversa, anexe também o `plano-aprovacao-prf.html`, e diga o que
> quer mudar. Contém: contexto, decisões de projeto, arquitetura técnica e ideias futuras.

---

## 1. O que é

Um sistema de estudos pessoal, em **um único arquivo HTML** (HTML + CSS + JS puro, sem
dependências externas exceto uma fonte do Google Fonts), para um candidato ao concurso da
**Polícia Rodoviária Federal (PRF)**. Roda 100% no navegador, salva dados localmente, é
gratuito e de uso pessoal. Não precisa de servidor, login, GitHub ou build.

Arquivo principal: `plano-aprovacao-prf.html` (a versão final; houve v1→v4 na evolução).

## 2. Perfil do usuário (para calibrar qualquer ajuste)

- Estuda pelo curso **Gran** (curso "2 em 1 PF e PRF - Pré-edital").
- Rotina real: ~1h de revisão de manhã (antes do expediente) + ~1h a 1h30 à noite, de seg a
  sex; sábado ~3h; domingo ~1h20. Total ~13–15h/semana.
- Assiste videoaulas em 2.0x–2.5x; troca de disciplina a cada 2 videoaulas (regra do Gran).
- Usa muito o **NotebookLM** (áudio overview, flashcards, quiz) — incorporado ao fluxo.
- Começou os estudos por volta de 27/06/2026; ~1 mês de estudo quando o sistema foi criado.
- Disposto a aumentar horas, desde que o acréscimo seja estratégico.

## 3. Fatos do concurso (base de todas as decisões)

Fonte: edital PRF nº 1/2021 (Cebraspe), que é o último vigente. Não há edital novo
publicado; previsão de publicação em **2027** (verificado em jul/2026). Estimativa de
8–14 meses de preparação até a prova.

Estrutura da prova objetiva (Cebraspe, estilo Certo/Errado, 120 itens, 4h30):
- **Bloco I — 55 itens** — corte mínimo 15,00 pts. Matérias: Língua Portuguesa, Raciocínio
  Lógico-Matemático, Informática, Física, Ética e Cidadania, Geopolítica, Inglês/Espanhol.
- **Bloco II — 30 itens** — corte 10,00 pts. Só Legislação de Trânsito (CTB + Resoluções CONTRAN).
- **Bloco III — 35 itens** — corte 10,00 pts. Direito Administrativo, Constitucional, Penal,
  Processual Penal, Legislação Especial, Direitos Humanos.
- Corte global: **50,00 pts** no conjunto dos 3 blocos.
- Correção Cebraspe: item certo **+1**, errado **−1**, branco/duplo **0**.
- Discursiva: até 30 linhas, 20 pts, eliminado se < 10. Fórmula: **NPD = NC − 4 × (NE ÷ TL)**
  (NC = nota de conteúdo, NE = nº de erros de forma, TL = linhas escritas). Fuga ao tema zera.
- Desempate na 1ª etapa favorece, nesta ordem: maior nota no Bloco II, depois Bloco III,
  depois Bloco I. (Por isso Trânsito e Direito "valem mais" no fio da navalha.)
- Etapas posteriores: TAF, avaliação psicológica, saúde, títulos, investigação social, CFP.

Progresso do usuário no Gran quando o sistema foi montado (% conclusão):
Geopolítica 50, Direitos Humanos 18, Ética 17, Const. 16, Física 15, Adm. 14, Port. 11,
Leg. Especial 11, Inglês 9, Trânsito 7, RLM 5, Penal+ProcPenal 5, Informática 4, Redação 100.
Matérias no painel do Gran que **NÃO caem no edital** (ignorar): Estatística, Inteligência
Emocional, Contabilidade Geral.

Total de videoaulas no curso Gran (usado no "orçamento de aulas"): 1.099 no total.
Por matéria: Const 62, Adm 71, Penal/PP 208, Trânsito 150, Port 90, Info 279, RL 202,
Leg.Esp 73, Física 55, Ética 48, DH 44, Inglês 55, Geo 16, Redação 7.
Insight-chave: Informática (279) + RL (202) = 481 aulas ≈ metade do curso, para matérias de
baixo peso no Bloco I. Assistir tudo é matematicamente incompatível com o prazo → cortar cauda.

## 4. Filosofia / métodos aplicados (não inventar "técnicas secretas")

As únicas técnicas realmente validadas para Cebraspe, e que o sistema implementa:
1. **Questões desde o primeiro assunto** (não só teoria; teoria sem questão dá falsa sensação de saber).
2. **Treino de abstenção** — como errar vale −1 e branco vale 0, treinar a NÃO marcar quando a
   segurança é baixa. Métrica principal = saldo líquido (acertos − erros), não % de acerto.
3. **Caderno de erros que realimenta revisão** — cada erro entendido vira revisão em +2 dias.
4. **Cortar cauda longa** — priorizar Bloco III (desempate) e Trânsito (30 itens/bloco);
   cortar excesso de Informática/RL.
5. **Revisão espaçada** — cada assunto volta em +1/+7/+21/+45 dias, em questões/áudio, não releitura.

Tom honesto mantido em todas as versões: nenhum sistema aprova ninguém; ele organiza e mede,
a execução diária é do usuário; não fomentar dependência da ferramenta.

## 5. As 3 fases (curva de horas automática)

- **Fase 1 — Fundação (~14h/sem):** agora até o edital sair. Cobrir núcleo do edital 1x com
  questões desde o início. 2 aulas/dia, 15 questões/sessão, redação quinzenal, simulado por bloco.
- **Fase 2 — Aprofundamento (~17h/sem):** quando o edital sair. Acréscimo vai 100% para
  questões/revisão. 1 aula/dia, 25 questões/sessão, redação semanal, simulado completo mensal.
- **Fase 3 — Reta final (~20h/sem):** ~8 semanas antes da prova. 35 questões/sessão, simulado
  completo semanal, redação semanal, caderno de erros diário, pouca aula.

O usuário troca de fase manualmente (barra no topo / aba Fases). "Hoje" e "Semana" se ajustam
à fase ativa (metas de questões, mix aula/questão, frequência de redação/simulado).

## 6. Arquitetura técnica (para adaptar o código)

- Arquivo único. Tudo dentro de um wrapper `<div class="prf">` com CSS scopeado por `.prf`.
- **Persistência:** usa `window.storage` (API get/set/list/delete, assíncrona, key-value,
  escopo por usuário, dados em JSON string). Chave atual: `'prf-v4-state'`.
  - IMPORTANTE: se for adaptar para rodar FORA deste ambiente (ex.: abrir como arquivo local
    solto no navegador), `window.storage` não existe. Trocar por `localStorage`
    (`localStorage.getItem/setItem`) OU manter e adicionar fallback. O backup exportar/importar
    (JSON via Blob + FileReader) já funciona em qualquer navegador e é a rede de segurança.
- **Estado (`st`):** `{ phase, lastSeen{}, prog{}, reviews[], questions[], errors[], reds[], sims[] }`.
- **Matérias (`S[]`):** cada item `{id, n(nome), b(bloco I/II/III), w(peso no bloco), p(%inicial),
  aulas(total no Gran), cap(teto sugerido de aulas)}`.
- **Priorização (`score`)**: `peso × atraso(=(100-prog)/100) × fatorTempo(=1+dias_sem_ver/10) ×
  pesoBloco(II=1.15, III=1.10, I=1.0)`. A matéria de maior score vira o "foco de hoje".
- **Revisão espaçada:** ao concluir sessão, cria review com `due = hoje + 1`, e ao revisar
  avança pelos estágios `REV=[1,7,21,45]`. Erros criam review `kind:'err'` com `due = hoje + 2`.
- **Abas:** Hoje, Fases, Semana, Aulas (orçamento), Questões, Erros, Redação & Simulados,
  Método, Backup. Troca via `.prf-tab[data-t]` → `.prf-panel#p-<t>`.
- **Design tokens (CSS vars):** `--nav:#0E2A47` (azul PRF), `--amber:#F4B93E` (faixa amarela),
  `--violet:#6C5CE7` (NotebookLM), `--g/--y/--r` (semáforo). Fontes: Barlow Condensed (títulos,
  ar de sinalização rodoviária), Inter (corpo), JetBrains Mono (números). Faixa tracejada
  amarela no header remete à sinalização de rodovia — é a "assinatura" visual.

## 7. Como pedir melhorias a uma IA (exemplos)

- "Troque `window.storage` por `localStorage` para eu rodar o HTML solto no meu PC."
- "Adicione um gráfico de evolução do saldo líquido ao longo do tempo na aba Questões."
- "Gere a ordem ideal das 14 disciplinas para eu reorganizar o arrastar-e-soltar do Gran"
  (subir Trânsito e Penal, que hoje estão mal posicionados na sequência do usuário).
- "Quando o edital sair, ative a Fase 2 por padrão e recalibre as metas para a data X da prova."
- "Adicione metas semanais de quantidade de questões por bloco e um alerta se eu ficar abaixo."
- "Crie um modo de simulado cronometrado dentro do próprio sistema."

## 8. Pendências / próximos passos sugeridos

- Ordem ideal das disciplinas no cronograma do Gran (não foi entregue ainda).
- Quando o edital novo sair: reconfirmar conteúdo programático (pode mudar levemente do de
  2021) e recalcular a contagem regressiva até a data da prova.
- Considerar exportar backup automático mensal (lembrete).

---
*Gerado como material de retomada. O arquivo funcional é o `plano-aprovacao-prf.html`.*
