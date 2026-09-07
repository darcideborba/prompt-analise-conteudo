# PROTOCOLO EXECUTÁVEL: análise de conteúdo aplicada a revisão de literatura

**Destinatário deste arquivo: agente de IA com acesso a shell, Python e sistema de arquivos.**
**Modo de uso: execute as fases na ordem. Não pule fases. Não prossiga com um gate reprovado.**
**Documento irmão: o protocolo de análise bibliométrica. Este cobre a camada qualitativa; aquele cobre a camada estrutural. Podem ser usados juntos ou isoladamente.**

---

## 0. OBJETIVO E CONTRATO

Você vai conduzir a análise de conteúdo de um corpus de artigos científicos dentro de uma revisão de literatura, do desenho do protocolo à síntese temática, produzindo: protocolo de revisão, planilha de triagem, dados completos do diagrama PRISMA 2020, codebook versionado, matriz conceito-documento, tabelas de síntese, relatório de confiabilidade e registro de decisões.

A técnica segue a análise de conteúdo na acepção de Krippendorff (2018) e Bardin (2016), com a distinção entre abordagem dedutiva e indutiva de Hsieh e Shannon (2005), Elo e Kyngäs (2008) e Mayring (2014), e a operacionalização em revisões de literatura de Tranfield, Denyer e Smart (2003), Denyer e Tranfield (2009), Webster e Watson (2002), Wolfswinkel, Furtmueller e Wilderom (2013) e Okoli (2015). O relato do fluxo segue o PRISMA 2020 (Page et al., 2021a, 2021b).

### 0.1 Regras invioláveis

Violá-las invalida a análise.

1. **NUNCA codifique antes de existir codebook escrito.** Sem definição prévia, o que você produz é impressão, não codificação.
2. **NUNCA altere uma definição de categoria sem versionar o codebook e recodificar o que já foi codificado sob a definição antiga.**
3. **NUNCA reporte confiabilidade sem dizer como foi obtida.** Codificador único significa "confiabilidade não estimada", e é isso que se escreve.
4. **NUNCA calcule coeficiente de concordância contra um comparador que você não auditou.** Ver 7.3.
5. **NUNCA atribua a um documento um código cuja evidência você não consiga citar.** Toda atribuição carrega o trecho que a sustenta.
6. **NUNCA infira do resumo aquilo que exige o texto completo.** Marque como pendente e declare no PRISMA.
7. **NUNCA preencha uma lacuna por suposição.** Toda lacuna vira pergunta ao usuário, conforme 0.2.
8. **NUNCA declare saturação sem o critério numérico que a define.** Ver 5.6.
9. **Ao final de cada fase, execute o gate e reporte o resultado antes de prosseguir.**
10. **Declare o uso de IA na codificação**, com a divisão exata entre o que a máquina propôs e o que o humano verificou, conforme Gatrell et al. (2024) e a política do periódico de destino.

### 0.2 MECANISMO DE LACUNA CONVERTIDA EM PERGUNTA

Este é o mecanismo central do protocolo. **Toda informação ausente, ambígua ou decidível apenas pelo pesquisador vira pergunta ao usuário no chat.** Não presuma, não invente, não adote silenciosamente um padrão.

Regras de operação:

1. **Agrupe as perguntas.** Faça-as em blocos, no início de cada fase, e não uma a uma. Interromper a cada dúvida é ruído.
2. **Ofereça opções sempre que possível.** Use componente de múltipla escolha se disponível. Cada opção deve trazer a consequência da escolha, não apenas o rótulo.
3. **Recomende uma opção**, marcando-a, e diga por quê em uma linha.
4. **Declare o padrão e o custo de não responder.** Se houver padrão defensável, informe-o: "se você não responder, adoto X, que implica Y".
5. **Bloqueie quando a decisão for irreversível ou definidora de escopo.** Nestes casos não há padrão: pare e espere.
6. **Registre pergunta e resposta** em `07_decisoes/log_decisoes.md`, com data. A resposta do usuário é dado de auditoria.
7. **Se o usuário estiver ausente ou a sessão for automatizada**, adote o padrão declarado, escreva no topo do produto qual interpretação foi usada, e liste as perguntas pendentes ao final para revisão.

Formato de cada pergunta:

```
[Q-nn] <pergunta objetiva>
  Contexto: <por que isso importa para o resultado>
  Opções:
    a) <opção> -> <consequência>
    b) <opção> -> <consequência>  [RECOMENDADA porque ...]
  Padrão se não houver resposta: <opção ou BLOQUEIA>
```

### 0.3 BLOCO DE PERGUNTAS INICIAIS

Faça este bloco antes de qualquer execução. As marcadas com BLOQUEIA impedem o início.

```
[Q-01] Já existe codebook para este projeto?
  Contexto: define se a Fase 5 valida um instrumento existente ou constroi um novo.
  Opções:
    a) Sim, tenho o codebook -> envie o arquivo; eu valido a estrutura contra 5.2 e
       aponto lacunas, sem alterar suas definicoes sem autorizacao
    b) Nao, proponha um -> eu construo a partir das perguntas de pesquisa e do
       referencial teorico que voce indicar, e submeto a sua aprovacao antes de codificar
    c) Existe parcialmente -> envie o que tem; eu completo e marco o que acrescentei
  Padrao se nao houver resposta: BLOQUEIA. Nao codifique sem instrumento.

[Q-02] Qual a abordagem de categorizacao?
  Contexto: determina a ordem entre teoria e dados (Hsieh e Shannon, 2005).
  Opcoes:
    a) Dedutiva (direcionada) -> categorias derivadas de teoria existente, aplicadas ao corpus
    b) Indutiva (convencional) -> categorias emergem do corpus, sem grade previa
    c) Mista, a priori mais a posteriori -> grade teorica inicial aberta a categorias
       emergentes  [RECOMENDADA em revisoes de literatura: preserva ancoragem teorica
       e permite achado nao previsto]
  Padrao se nao houver resposta: c

[Q-03] Quais sao as perguntas de pesquisa, na formulacao final?
  Contexto: as categorias a priori derivam delas. Sem elas a grade nao tem origem
  defensavel.
  Padrao: BLOQUEIA.

[Q-04] Qual o referencial teorico que orienta as categorias a priori?
  Contexto: em revisao dedutiva, as categorias vem de teoria nomeada, nao de intuicao.
  Padrao: BLOQUEIA se a resposta a Q-02 for (a) ou (c).

[Q-05] Qual a unidade de analise e a unidade de codificacao?
  Contexto: Krippendorff (2018) distingue unidade de amostragem, de registro e de
  contexto. Confundi-las inviabiliza a contagem.
  Opcoes:
    a) Documento inteiro como unidade de registro  [RECOMENDADA em revisao de literatura]
    b) Secao (metodo, resultados, discussao)
    c) Paragrafo ou trecho
  Padrao: a

[Q-06] Ha protocolo de revisao previamente registrado (PROSPERO, OSF, outro)?
  Contexto: altera o que pode ser mudado no meio do caminho e o que deve ser
  declarado como desvio de protocolo.
  Padrao: assumir que nao ha, e registrar as decisoes internamente.

[Q-07] Quantos codificadores participarao?
  Contexto: define se ha confiabilidade estimavel (Fase 7).
  Opcoes:
    a) Um -> confiabilidade nao estimada; sera declarado como limitacao
    b) Dois ou mais independentes -> calcularemos coeficiente e resolveremos divergencias
    c) Um humano mais assistencia de IA -> exige declaracao especifica; ver 7.3 e 0.1.10
  Padrao: perguntar de novo; esta resposta muda o que pode ser reportado.

[Q-08] Qual o periodico ou banca de destino?
  Contexto: define limite de extensao, estilo de referencia, exigencia de PRISMA e
  politica de uso de IA, que pode proibir a redacao assistida.
  Padrao: prosseguir sem restricao, avisando que o produto pode nao caber no destino.

[Q-09] Ha limite de extensao e ele conta referencias, tabelas e figuras?
  Contexto: alguns periodicos contam tudo dentro do limite e cobram palavras por
  figura ou tabela. Isso muda o orcamento de sintese desde o inicio.
  Padrao: assumir que nao conta, e avisar que a conta pode mudar.

[Q-10] Como os documentos do corpus serao citados no texto final?
  Contexto: identificador interno (D001) serve ao trabalho; na redacao final exige-se
  citacao bibliografica normal, o que pode acrescentar dezenas de referencias.
  Opcoes:
    a) Citacao bibliografica normal desde o inicio  [RECOMENDADA: evita conversao
       cara no fim, que custa 30 a 40 palavras por entrada nova]
    b) Identificador interno agora, conversao depois
  Padrao: a
```

### 0.4 Estrutura de diretórios

```
projeto/
  00_protocolo/      protocolo_revisao.md, perguntas_pesquisa.md
  01_corpus/         registros_brutos.csv, triagem.xlsx, corpus_final.json
  02_codebook/       codebook_v1.md, codebook_v2.md, ... changelog.md
  03_codificacao/    codificacao.csv, evidencias.csv, memos/
  04_confiabilidade/ dupla_codificacao.csv, relatorio_confiabilidade.md
  05_sintese/        matriz_conceito_documento.csv, tabelas_sintese.xlsx
  06_prisma/         prisma_dados.json, prisma_checklist.md, Figura_PRISMA.png
  07_decisoes/       log_decisoes.md, perguntas_pendentes.md
```

---

## FASE 1: DEFINIR UNIDADES E NÍVEL DE ANÁLISE

Krippendorff (2018) distingue três unidades e a confusão entre elas é o erro de partida mais comum.

| Unidade | O que é | Escolha típica em revisão de literatura |
|---|---|---|
| Amostragem | o que entra no corpus | o artigo publicado |
| Registro | o que recebe um código | o artigo inteiro |
| Contexto | o que se lê para decidir o código | resumo mais seções relevantes, ou o texto integral |

Registre a escolha das três e a justificativa. Se a unidade de registro for menor que o documento, o número de unidades codificadas deixa de coincidir com o número de documentos, e todas as contagens posteriores mudam de denominador. Declare o denominador em toda tabela.

### GATE 1

```
[ ] as tres unidades estao definidas por escrito
[ ] o denominador de contagem esta declarado
[ ] as perguntas de pesquisa estao registradas em 00_protocolo/
```

---

## FASE 2: PROTOCOLO E CRITÉRIOS A PRIORI

Escreva o protocolo antes de ver os dados. É o que separa revisão sistemática de leitura assistemática (Tranfield, Denyer e Smart, 2003).

O protocolo contém: perguntas de pesquisa; bases e data da busca; string de busca literal por plataforma; critérios de inclusão e exclusão; unidades de análise; instrumento de extração; abordagem de categorização; procedimento de confiabilidade; e critérios de qualidade dos estudos.

**Critérios de inclusão** devem ser condições verificáveis contra o texto, não juízos. "Trata de transformação digital" não é verificável; "reporta ao menos uma variável organizacional observada, medida ou teorizada" é.

**Condição de inclusão composta.** Quando a revisão une duas literaturas, exija que o documento satisfaça simultaneamente a condição de cada bloco. Tabule a condição, porque ela é o instrumento reutilizável que permite a outro pesquisador decidir se um estudo pertence à mesma literatura.

**Códigos de exclusão** numerados, mutuamente excludentes, aplicados na ordem escrita, com definição operacional de cada um. Modelo genérico:

```
E1  atende um bloco conceitual mas nao o outro
E2  fora do objeto definido
E3  contexto inadequado (nivel, setor, populacao)
E4  tipo de documento inadequado
E5  idioma fora do escopo
E6  texto completo nao recuperado
```

Aplicar na ordem importa: um documento que satisfaz E1 e E4 é contado uma única vez, sob E1, e a soma dos códigos fecha com o total de exclusões.

**Perguntas desta fase:**

```
[Q-11] Os criterios de inclusao estao formulados como condicoes verificaveis?
  Se algum for juizo e nao condicao, eu proponho a reformulacao e submeto a voce.

[Q-12] Ha criterio de qualidade metodologica para excluir estudos, ou a inclusao
  independe da qualidade?
  Contexto: revisoes agregativas costumam excluir por qualidade; revisoes
  configurativas costumam incluir e ponderar (Gough, Oliver e Thomas, 2017).
  Opcoes:
    a) Excluir por qualidade -> defina o instrumento (AMSTAR 2, MMAT, CASP, outro)
    b) Incluir e reportar a qualidade como caracteristica  [RECOMENDADA em revisoes
       de teoria e agenda, onde ensaios conceituais sao evidencia legitima]
  Padrao: b, declarando a escolha.

[Q-13] Qual o recorte temporal e a justificativa?
  Padrao: sem recorte, declarando que a distribuicao anual sera reportada.
```

### GATE 2

```
[ ] protocolo escrito e datado
[ ] criterios de inclusao verificaveis, um a um
[ ] codigos de exclusao numerados, definidos e ordenados
[ ] string de busca transcrita literalmente por plataforma
```

---

## FASE 3: TRIAGEM

### 3.1 Lógica de três estados

Adote a lógica A, B, C de Pittaway et al. (2004). Não use binário.

- **A** inclusão pelo título e resumo
- **B** exige o texto completo para decidir
- **C** exclusão

A existência de B é o que impede que a dúvida seja resolvida por conveniência. Em caso de dúvida persistente após o texto completo, adote **regra conservadora declarada**: excluir na dúvida, ou incluir na dúvida. Declare qual, porque as duas são defensáveis e produzem corpus diferentes.

### 3.2 Campos obrigatórios por registro

```
id                identificador estavel (D001..Dnnn), imutavel
titulo, autores, ano, periodico, doi, base_origem
decisao           A | B | C
condicao_1..n     sim | nao | duvida, uma coluna por bloco conceitual
confianca         alta | media | baixa
codigo_exclusao   E1..En, vazio se incluido
justificativa     uma frase, especifica ao documento
texto_completo    procurado | nao procurado; recuperado | nao recuperado
fase_decisao      triagem | texto completo
```

**A justificativa é obrigatória e deve ser específica.** Justificativas repetidas literalmente em muitos registros são sinal de classificação por regra lexical e não por leitura. Ver 7.3.

### 3.3 Triagem em duas passagens

Passagem 1, sobre título e resumo, aplicando os critérios. Passagem 2, sobre o texto completo, apenas nos B. Nunca reclassifique um C sem registrar a mudança e o motivo no log de decisões.

### 3.4 Quando o texto completo não é recuperado

Registre individualmente. Não misture "não recuperado" com "não procurado". Se um documento foi decidido pelo resumo por indisponibilidade do texto, isso é uma limitação que entra no PRISMA e nas Limitações.

**Perguntas desta fase:**

```
[Q-14] Regra na duvida persistente: excluir ou incluir?
  Opcoes:
    a) Excluir na duvida -> corpus menor, mais especifico, risco de perder evidencia
    b) Incluir na duvida -> corpus maior, mais ruido, risco de diluir o achado
  Padrao: a, declarando a escolha. [RECOMENDADA quando o objeto e emergente e mal
  delimitado, porque a delimitacao e parte da contribuicao]

[Q-15] Como proceder com documentos cujo texto completo nao foi recuperado?
  Opcoes:
    a) Excluir e contar em E6
    b) Decidir pelo resumo, marcando individualmente  [RECOMENDADA se forem poucos]
  Padrao: b, com marcacao individual e declaracao no PRISMA.
```

### GATE 3

```
[ ] n_A + n_B + n_C == n_triados
[ ] soma dos codigos de exclusao == n_C
[ ] toda linha excluida tem exatamente um codigo
[ ] toda linha tem justificativa nao vazia
[ ] justificativas repetidas literalmente: reportar o percentual
[ ] nenhum id duplicado; nenhum id do corpus final ausente da triagem
```

---

## FASE 4: DADOS DO DIAGRAMA PRISMA 2020

O diagrama não é ilustração: é a prestação de contas aritmética do corpus. Gere-o a partir dos dados, nunca à mão.

### 4.1 Campos a extrair, na estrutura do PRISMA 2020

```json
{
  "identificacao": {
    "registros_por_base": {"Base1": 0, "Base2": 0},
    "registros_outras_fontes": {"citacoes": 0, "manual": 0, "listas_de_referencias": 0},
    "duplicados_removidos": 0,
    "removidos_por_automacao": 0,
    "removidos_outros_motivos": 0
  },
  "triagem": {
    "registros_triados": 0,
    "registros_excluidos": 0,
    "excluidos_por_codigo": {"E1": 0, "E2": 0, "E3": 0, "E4": 0, "E5": 0}
  },
  "elegibilidade": {
    "textos_completos_buscados": 0,
    "textos_completos_nao_recuperados": 0,
    "textos_completos_avaliados": 0,
    "textos_completos_excluidos": 0,
    "excluidos_no_texto_completo_por_motivo": {"motivo": 0}
  },
  "inclusao": {
    "estudos_incluidos": 0,
    "relatos_incluidos": 0
  }
}
```

Distinga **estudos** de **relatos**: dois artigos sobre o mesmo estudo são um estudo e dois relatos. Em revisões de literatura de gestão a distinção costuma ser trivial, mas quando não for, ela muda o denominador.

### 4.2 Verificações aritméticas obrigatórias

Implemente como asserções no gerador, para que a inconsistência apareça no arquivo e não sobreviva até a revisão por pares.

```python
assert soma(registros_por_base) + soma(outras_fontes) - duplicados_removidos \
       - removidos_por_automacao - removidos_outros == registros_triados
assert registros_triados - registros_excluidos == textos_completos_buscados
assert textos_completos_buscados - nao_recuperados == textos_completos_avaliados
assert textos_completos_avaliados - excluidos_texto_completo == estudos_incluidos
assert soma(excluidos_por_codigo) == registros_excluidos
```

**Se alguma asserção falhar, pare.** Não ajuste um número para fechar a conta. Encontre a origem da divergência, corrija-a nos dados, e se a divergência for real e irredutível, declare-a explicitamente no material de apoio em vez de escondê-la.

### 4.3 Caminhos A e B não se somam

Erro frequente: somar os documentos lidos por inclusão direta com os lidos para decidir. São caminhos distintos. O documento A foi lido para a síntese qualitativa; o documento B foi lido para a decisão de inclusão. Modele os dois caminhos separadamente e não os conflacione em um número único de "textos completos avaliados".

### 4.4 Checklist PRISMA 2020

Preencha os 27 itens do checklist com a localização de cada um no manuscrito. Itens não aplicáveis recebem justificativa, não ficam em branco.

**Perguntas desta fase:**

```
[Q-16] Houve busca em outras fontes alem das bases (listas de referencias,
  busca manual, contato com autores, literatura cinzenta)?
  Contexto: o PRISMA 2020 exige o registro separado dessas vias.
  Padrao: assumir que nao, e declarar.

[Q-17] Houve uso de ferramenta de automacao na triagem?
  Contexto: o PRISMA 2020 pede o registro de registros removidos por automacao e
  a descricao da ferramenta.
  Padrao: perguntar, porque a resposta muda o campo removidos_por_automacao.
```

### GATE 4

```
[ ] as cinco assercoes de 4.2 passam
[ ] caminhos A e B modelados separadamente
[ ] checklist PRISMA 2020 preenchido com localizacao por item
[ ] diagrama gerado a partir do JSON, nao desenhado a mao
```

---

## FASE 5: CODEBOOK

### 5.1 PERGUNTA OBRIGATÓRIA ANTES DE QUALQUER COISA

Se ainda não perguntou em Q-01, pergunte agora e espere a resposta.

```
[Q-01] Ja existe codebook para este projeto, ou devo propor um?
```

**Se existir**, não o altere. Valide a estrutura contra 5.2, liste as lacunas encontradas e pergunte, item a item, se deseja complementá-lo. Alterar o instrumento do pesquisador sem autorização invalida a comparabilidade com codificações anteriores.

**Se não existir**, construa e submeta à aprovação antes de codificar qualquer documento. Um codebook não aprovado não é instrumento, é rascunho.

### 5.2 Estrutura mínima de cada entrada

Siga DeCuir-Gunby, Marshall e McCulloch (2011) e MacQueen et al. (1998). Cada código traz seis campos, e um codebook sem eles não é auditável.

```
codigo            rotulo curto e estavel
definicao         o que o codigo significa, em uma frase
quando_aplicar    criterio de inclusao, operacional
quando_nao_aplicar criterio de exclusao, com a distincao dos codigos vizinhos
exemplo_positivo  trecho real do corpus que recebe o codigo
exemplo_negativo  trecho real que poderia parecer, mas nao recebe
origem            a priori (com a fonte teorica) | a posteriori (com o documento
                  em que emergiu)
versao            em que versao do codebook entrou ou mudou
```

O campo **quando_nao_aplicar** é o que mais evita divergência entre codificadores, e é o mais frequentemente omitido. Escreva-o sempre, nomeando o código vizinho de que se distingue.

### 5.3 Categorias a priori (dedutivas)

Derivam da teoria e das perguntas de pesquisa, e são escritas antes do contato com os dados (Mayring, 2014; Elo e Kyngäs, 2008).

Procedimento: para cada pergunta de pesquisa, identifique os construtos que ela mobiliza; para cada construto, escreva a definição adotada com a fonte; converta a definição em critério observável no texto; e só então formule o código.

Um erro comum é derivar categorias do que se espera encontrar, e não do que a teoria define. Ancore cada categoria a priori em uma referência nomeada, e registre-a no campo `origem`. Se você não consegue nomear a fonte, a categoria é a posteriori disfarçada.

### 5.4 Categorias a posteriori (indutivas)

Emergem da leitura (Hsieh e Shannon, 2005, abordagem convencional; Braun e Clarke, 2006; Saldaña, 2021).

Procedimento em duas voltas. Na primeira, codifique um subconjunto do corpus com codificação aberta, gerando códigos descritivos próximos ao texto, sem forçá-los na grade a priori. Na segunda, agrupe os códigos abertos por similaridade semântica em categorias, e as categorias em temas, no movimento de primeira e segunda ordem descrito por Gioia, Corley e Hamilton (2013).

**Registre a proveniência de toda categoria emergente**: em que documento apareceu, em que trecho, e em que versão do codebook entrou. Sem isso, o leitor não distingue achado de invenção.

**Tamanho do subconjunto inicial**: entre 10% e 20% do corpus, ou o mínimo de 10 documentos, o que for maior. Selecione com variação deliberada, cobrindo anos, tipos de evidência e subáreas, e não os primeiros da lista.

### 5.5 Abordagem mista

Em revisão de literatura, a combinação costuma ser superior às duas puras. A grade a priori dá ancoragem teórica e comparabilidade; a abertura indutiva permite o achado não previsto, que é frequentemente o que justifica a publicação.

Operacionalmente: aplique a grade a priori e mantenha uma categoria residual explícita, do tipo "não classificável na grade atual". Quando essa residual acumular além de um limiar declarado, ela é sinal de que a grade está incompleta, e o conteúdo dela é a matéria-prima das categorias a posteriori.

```
[Q-18] Qual o limiar de acionamento da revisao da grade?
  Contexto: quando a categoria residual cresce, a grade precisa mudar.
  Opcoes:
    a) 10% das unidades codificadas  [RECOMENDADA]
    b) 20%
    c) Revisar apenas ao final
  Padrao: a
```

### 5.6 Saturação

Não declare saturação sem critério numérico. Critério operacional recomendado: nenhuma categoria nova em N documentos consecutivos, com N entre 10 e 15, ou 10% do corpus, o que for maior. Registre em que documento a saturação foi atingida e continue codificando o restante, porque saturação de categorias não dispensa a codificação completa.

### 5.7 Versionamento

Toda mudança gera nova versão do codebook e uma entrada no changelog com: o que mudou, por quê, quantos documentos precisam de recodificação, e se a recodificação foi feita.

**Regra dura**: mudar a definição de um código e não recodificar o que foi codificado sob a definição antiga produz um conjunto de dados internamente inconsistente. Se a recodificação for inviável, declare quantos registros permanecem sob a definição anterior.

**Perguntas desta fase:**

```
[Q-19] Aprova o codebook proposto?
  Apresente: numero de codigos, arvore de categorias, e as tres definicoes que
  considera mais dificeis de aplicar. Peca aprovacao explicita antes de codificar.
  Padrao: BLOQUEIA.

[Q-20] Quantos niveis a arvore de categorias deve ter?
  Opcoes:
    a) Dois: categoria e codigo
    b) Tres: dimensao, categoria e codigo  [RECOMENDADA quando ha mais de 20 codigos]
  Padrao: b se n_codigos > 20, senao a.
```

### GATE 5

```
[ ] codebook aprovado pelo usuario, com data
[ ] todo codigo tem os seis campos de 5.2, incluindo quando_nao_aplicar
[ ] todo codigo a priori tem fonte teorica nomeada
[ ] todo codigo a posteriori tem documento e trecho de origem
[ ] nao ha dois codigos com definicoes sobrepostas: cheque par a par
[ ] existe categoria residual explicita
```

---

## FASE 6: CODIFICAÇÃO E EXTRAÇÃO

### 6.1 Ficha de extração

Além dos códigos, extraia de cada documento os campos que sustentam a síntese. Conjunto mínimo, adaptável:

```
id, ano, periodico, pais_do_estudo
tipo_de_documento      empirico | conceitual | revisao | ensaio | nota tecnica
desenho                survey | experimento | caso | etnografia | modelagem |
                       longitudinal | design science | nao aplicavel
nivel_de_analise       individuo | equipe | processo | unidade | organizacao |
                       cadeia | campo | pais
fonte_de_dados         primaria | secundaria | simulada | nao aplicavel
amostra                descricao e tamanho
teoria_mobilizada      nomeada, ou "nenhuma explicita"
construtos             lista
achado_principal       uma frase, nas palavras do proprio artigo quando possivel
limitacao_declarada    uma frase
codigos_atribuidos     lista de codigos do codebook
evidencia_por_codigo   trecho literal que sustenta cada atribuicao, com localizacao
```

O campo **teoria_mobilizada** merece atenção: registrar "nenhuma teoria explícita" é um dado, e a frequência dessa marcação costuma ser um dos achados mais fortes de revisões sobre campos emergentes.

### 6.2 Evidência obrigatória

Toda atribuição de código carrega o trecho que a sustenta e sua localização. Sem isso a codificação não é verificável e a síntese não é rastreável.

Grave em `03_codificacao/evidencias.csv` com: `id`, `codigo`, `trecho`, `localizacao`, `codificador`, `data`, `confianca`.

### 6.3 Memos

Escreva memos analíticos durante a codificação, não depois (Miles, Huberman e Saldaña, 2020; Saldaña, 2021). Um memo registra dúvida de aplicação, hipótese sobre padrão emergente, tensão entre documentos, ou decisão de fronteira. São eles que se convertem em interpretação na Fase 9.

### 6.4 Codificação assistida por IA

Se houver assistência de IA, valem quatro regras.

Primeira, os critérios devem estar escritos **antes**, e a máquina aplica o codebook, não o cria sem supervisão. Segunda, **toda classificação retornada é verificada por humano contra o texto** antes de ser registrada. Terceira, registre a calibração: um conjunto de documentos com classificação conhecida de antemão, usado para checar o comportamento do procedimento. Quarta, declare o uso, com a divisão exata entre o proposto e o verificado, conforme Gatrell et al. (2024).

**Atenção à política do periódico.** Vários editores permitem a IA como auxílio à análise, com declaração transparente, e proíbem a geração de texto do manuscrito. Verifique antes, porque a distinção entre auxiliar a análise e redigir o artigo é a linha que separa o permitido do não permitido.

### GATE 6

```
[ ] todo documento incluido tem ficha de extracao completa
[ ] todo codigo atribuido tem evidencia com localizacao
[ ] nenhum documento sem nenhum codigo, salvo os marcados como residuais
[ ] frequencia de cada codigo calculada e revisada: codigos com frequencia zero
    devem ser removidos ou justificados; codigos com frequencia proxima de 100%
    nao discriminam e devem ser revistos
[ ] memos gravados em 03_codificacao/memos/
```

---

## FASE 7: CONFIABILIDADE

### 7.1 Escolha do coeficiente

| Situação | Coeficiente | Referência |
|---|---|---|
| Dois codificadores, categorias nominais | Kappa de Cohen | Cohen (1960) |
| Dois ou mais, dados faltantes, qualquer nível de medida | Alpha de Krippendorff | Krippendorff (2004, 2018) |
| Concordância bruta | percentual de acordo | reportar apenas junto com um dos acima |

Percentual de acordo isolado **não** é medida de confiabilidade, porque não corrige a concordância esperada por acaso. Nunca o reporte sozinho.

### 7.2 Limiares de interpretação

Para o alpha de Krippendorff, Krippendorff (2004) recomenda α ≥ 0,800 para conclusões firmes e admite 0,667 como piso para conclusões tentativas. Para o kappa, os rótulos de Landis e Koch (1977) são convenção difundida, e devem ser usados como referência descritiva e não como aprovação automática.

Reporte o coeficiente **por código**, e não apenas o global. Um alpha global aceitável pode esconder um código específico com concordância nula, e é justamente esse código que precisa de redefinição.

### 7.3 Auditoria do comparador antes de calcular

**Regra dura.** Antes de calcular qualquer coeficiente contra uma segunda codificação, audite-a. Sinais de que a segunda codificação não veio de leitura:

```
[ ] as justificativas se repetem literalmente em mais de 60% dos casos
[ ] a decisao e previsivel por uma regra lexical simples, do tipo presenca de
    palavra-chave, testada sobre uma amostra
[ ] a concordancia e alta nos casos faceis e proxima de zero nos dificeis
[ ] o tempo de producao e incompativel com a leitura do material
```

Se algum sinal se confirmar, **o coeficiente calculado mede a inadequação do comparador, e não a confiabilidade da sua codificação.** Reporte a verificação como tentada e inválida, com a evidência da auditoria, e declare a confiabilidade como não estimada. Isso é mais honesto e mais defensável do que apresentar um número obtido contra um comparador ruim.

### 7.4 Codificador único

É situação comum e não desqualifica a revisão, desde que declarada. Escreva "a triagem e a codificação foram conduzidas por um único revisor, e a confiabilidade entre codificadores não foi estimada", e traga isso para as Limitações, com a indicação do que uma replicação precisaria fazer.

Mitigações que devem ser adotadas e relatadas: recodificação de uma amostra pelo mesmo codificador após intervalo (estabilidade intra-codificador), critérios escritos antes, evidência por atribuição, e registro de decisões de fronteira.

### 7.5 Resolução de divergências

Quando houver dois codificadores, registre o procedimento: discussão até consenso, decisão de terceiro, ou regra pré-definida. Registre também quantas divergências ocorreram e em que códigos, porque a distribuição das divergências indica quais definições estão frágeis.

**Perguntas desta fase:**

```
[Q-21] Qual percentual do corpus sera duplamente codificado?
  Opcoes:
    a) 10%  b) 20%  [RECOMENDADA]  c) 100%
  Padrao: b, com selecao aleatoria estratificada por ano e tipo de documento.

[Q-22] Como resolver divergencias?
  Opcoes:
    a) Discussao ate consenso  [RECOMENDADA]
    b) Terceiro codificador decide
    c) Regra pre-definida
  Padrao: a
```

### GATE 7

```
[ ] comparador auditado antes do calculo
[ ] coeficiente reportado global E por codigo
[ ] limiar adotado declarado com a fonte
[ ] divergencias contadas por codigo
[ ] se codificador unico: declaracao explicita, nao omissao
```

---

## FASE 8: MATRIZ CONCEITO-DOCUMENTO

Webster e Watson (2002) estabelecem que a revisão deve ser centrada em conceitos, e não em autores. A matriz é o instrumento dessa virada.

Construa `05_sintese/matriz_conceito_documento.csv`, com documentos nas linhas e conceitos nas colunas, marcando presença, ausência e, quando aplicável, direção ou intensidade do achado.

A matriz responde imediatamente a três perguntas que a leitura sequencial não responde: quais conceitos estão saturados e quais estão vazios; quais combinações de conceitos nunca foram estudadas juntas; e quais documentos são atípicos por combinarem conceitos que os demais não combinam.

**As células vazias são o achado.** Uma coluna com poucas marcações é uma lacuna, e lacunas com significado teórico são a matéria-prima da agenda de pesquisa. Reporte explicitamente as combinações de conceitos ausentes.

Derive daí as tabelas de síntese:

| Tabela | Conteúdo |
|---|---|
| Distribuição por categoria | frequência e percentual de cada código |
| Cruzamento categoria por ano | evolução temporal das categorias |
| Cruzamento categoria por tipo de evidência | que categorias têm evidência empírica e quais são só conceituais |
| Cruzamento categoria por nível de análise | em que nível cada tema foi estudado |
| Teorias mobilizadas | frequência, incluindo "nenhuma explícita" |
| Lacunas | combinações ausentes ou raras, com interpretação |

O cruzamento entre categoria e tipo de evidência é o mais informativo em campos emergentes: ele mostra onde a literatura afirma sem medir.

### GATE 8

```
[ ] matriz completa, sem celulas indefinidas
[ ] soma das frequencias por codigo confere com a codificacao
[ ] tabela de lacunas produzida e interpretada
[ ] toda tabela declara o denominador
```

---

## FASE 9: SÍNTESE TEMÁTICA

Da descrição à interpretação. Siga a síntese temática de Thomas e Harden (2008), com a estrutura de primeira e segunda ordem de Gioia, Corley e Hamilton (2013).

Três movimentos.

**Primeiro, descrever.** Para cada categoria: quantos documentos, que tipo de evidência predomina, o que a literatura afirma, e onde ela diverge. Divergência entre documentos é achado, não ruído a ser aparado. Nomeie os documentos que discordam e explicite a tensão.

**Segundo, interpretar.** Agrupe as categorias descritivas em temas analíticos que digam algo que nenhum documento isolado diz. É aqui que a revisão passa de inventário a contribuição.

**Terceiro, confrontar com a teoria.** Para cada lente teórica mobilizada, estabeleça o estado da relação entre ela e o corpus. Um vocabulário útil, extraído da prática:

```
presente e ativa    a teoria e aplicada e o corpus a desenvolve
presente e inerte   a teoria e citada como rotulo, sem que seus mecanismos
                    sejam operacionalizados
presente e nao revisada  a teoria e estendida a um objeto novo sem que o objeto
                    force revisao dos seus pressupostos
ausente             a teoria seria pertinente e nao aparece
```

Essa classificação é frequentemente o achado teórico central de uma revisão, porque "citada como rótulo e não desenvolvida" é um diagnóstico diferente de "ausente", e ambos são diferentes de "aplicada".

**Regra de rastreabilidade**: toda afirmação da síntese remete aos documentos que a sustentam. Uma afirmação sem lastro identificável é opinião do revisor, e se for para constar, deve constar como tal.

### GATE 9

```
[ ] cada tema remete aos documentos que o sustentam
[ ] divergencias entre documentos declaradas, nao aparadas
[ ] estado de cada lente teorica classificado e justificado
[ ] nenhuma afirmacao sem lastro
```

---

## FASE 10: DA SÍNTESE À AGENDA DE PESQUISA

A agenda não é lista de sugestões: é derivada das lacunas que a análise expôs. Cada pergunta proposta deve ser rastreável a uma célula vazia da matriz ou a uma tensão identificada na síntese.

Estruture cada pergunta com cinco atributos:

```
lacuna         o que a analise expos, com referencia aos documentos
pergunta       formulada de modo pesquisavel
natureza       explorativa (transfere teoria nao usada) | exploitativa (aprofunda
               teoria ja em uso)
pertinencia    especifica (interna a uma categoria) | holistica (dirigida ao campo)
lente          a teoria mobilizada
nivel          o nivel de analise em que a pergunta se responde
```

Declare quais perguntas você priorizaria e por quê. Uma agenda sem hierarquia transfere ao leitor um trabalho que era do revisor.

---

## FASE 11: QUALIDADE E AVALIAÇÃO

Avalie a própria revisão contra instrumento reconhecido. AMSTAR 2 (Shea et al., 2017) para revisões com pretensão sistemática; o checklist PRISMA 2020 para o relato; e os critérios de Templier e Paré para revisões em sistemas de informação e gestão.

Registre a autoavaliação item a item, incluindo os itens não atendidos. Uma autoavaliação sem item reprovado é sinal de que a avaliação não foi feita com seriedade.

Classifique também o tipo de revisão que você produziu, seguindo Paré et al. (2015), e verifique se os procedimentos adotados correspondem ao tipo declarado. Uma revisão declarada sistemática com busca em base única e sem critérios escritos é uma revisão narrativa mal rotulada.

---

## FASE 12: REPORTE E TRANSPARÊNCIA

### 12.1 O que vai no corpo do artigo

Método com: desenho da revisão e protocolo seguido; bases, data e string de busca; critérios de inclusão e exclusão com os códigos; procedimento de triagem em três estados; abordagem de categorização, dedutiva, indutiva ou mista; origem das categorias a priori; procedimento de emergência das a posteriori; confiabilidade, com o coeficiente ou a declaração de não estimação; e o uso de IA, se houver.

### 12.2 O que vai no material de apoio

Protocolo completo, string literal por plataforma, codebook em todas as versões com changelog, planilha de triagem com todas as decisões e justificativas, dados do PRISMA em formato estruturado, checklist PRISMA preenchido, matriz conceito-documento, evidências por atribuição, relatório de confiabilidade e log de decisões.

### 12.3 Registro de decisões

`07_decisoes/log_decisoes.md`, com uma entrada por decisão: data, decisão, alternativas consideradas, motivo, e quem decidiu. As respostas do usuário às perguntas deste protocolo entram aqui.

Este registro é o que permite responder à pergunta do revisor "por que vocês fizeram assim" sem reconstruir a memória meses depois.

---

## 13. ARMADILHAS

Cada item abaixo ocorreu de fato em projetos reais. Cheque um a um antes de entregar.

1. **Codificar antes de escrever o codebook.** O que se produz é impressão, e ela não é replicável.
2. **Categoria sem `quando_nao_aplicar`.** É a omissão que mais gera divergência entre codificadores.
3. **Mudar a definição de um código e não recodificar o que já foi codificado.** Produz base internamente inconsistente.
4. **Categoria a posteriori sem registro de proveniência.** O leitor não distingue achado de invenção.
5. **Calcular coeficiente contra comparador não auditado.** Ver 7.3.
6. **Reportar percentual de acordo isolado** como se fosse confiabilidade.
7. **Reportar apenas o coeficiente global**, escondendo o código com concordância nula.
8. **Somar os caminhos A e B no PRISMA.** São caminhos distintos.
9. **Ajustar um número para a conta do PRISMA fechar.** Encontre a causa; se a divergência for real, declare-a.
10. **Confundir "não recuperado" com "não procurado".**
11. **Declarar saturação sem critério numérico.**
12. **Aparar divergências entre documentos** para produzir uma síntese lisa. A divergência é o achado.
13. **Afirmar na síntese o que nenhum documento sustenta.** Toda afirmação tem lastro identificável.
14. **Agenda de pesquisa não rastreável às lacunas.** Vira lista de sugestões genéricas.
15. **Citar documentos do corpus por identificador interno na versão final.** O identificador serve ao trabalho; na redação use citação bibliográfica normal. Converter no fim é caro: 30 a 40 palavras por entrada nova, mais a expansão no corpo, e pode exigir sufixos de ano em homônimos.
16. **Deixar no texto afirmação sobre análise pendente depois de executá-la.** Releia o manuscrito inteiro contra o estado final, não só as seções recém-editadas.
17. **Autoavaliação de qualidade sem nenhum item reprovado.** Sinal de avaliação não feita.
18. **Presumir em vez de perguntar.** Toda lacuna vira pergunta, conforme 0.2.

---

## 14. BANCO CONSOLIDADO DE PERGUNTAS

Perguntas que **bloqueiam** o início: Q-01 codebook existente, Q-03 perguntas de pesquisa, Q-04 referencial teórico (se abordagem dedutiva ou mista), Q-19 aprovação do codebook.

Perguntas com padrão declarado: Q-02 abordagem, Q-05 unidades, Q-06 registro de protocolo, Q-08 destino, Q-09 limite de extensão, Q-10 forma de citação, Q-12 critério de qualidade, Q-13 recorte temporal, Q-14 regra na dúvida, Q-15 texto não recuperado, Q-16 outras fontes, Q-17 automação, Q-18 limiar de revisão da grade, Q-20 níveis da árvore, Q-21 percentual de dupla codificação, Q-22 resolução de divergências.

Pergunta que exige resposta explícita: Q-07 número de codificadores, porque determina o que pode ser reportado.

**Gere perguntas adicionais sempre que encontrar**: campo ausente na exportação que a ficha de extração exige; critério de inclusão que não é verificável contra o texto; documento cujo enquadramento não é decidível pelo codebook atual; categoria emergente que se sobrepõe a uma existente; divergência aritmética no PRISMA; conflito entre a política do periódico e o procedimento adotado; ou qualquer decisão que altere o escopo do corpus.

---

## 15. LITERATURA DE RESPALDO

**Análise de conteúdo e codificação**

Bardin, L. (2016). *Análise de conteúdo*. Edições 70.
Boyatzis, R.E. (1998). *Transforming Qualitative Information: Thematic Analysis and Code Development*. Sage.
Braun, V. e Clarke, V. (2006). Using thematic analysis in psychology. *Qualitative Research in Psychology*, 3(2), 77-101.
DeCuir-Gunby, J.T., Marshall, P.L. e McCulloch, A.W. (2011). Developing and using a codebook for the analysis of interview data. *Field Methods*, 23(2), 136-155.
Elo, S. e Kyngäs, H. (2008). The qualitative content analysis process. *Journal of Advanced Nursing*, 62(1), 107-115.
Hsieh, H.-F. e Shannon, S.E. (2005). Three approaches to qualitative content analysis. *Qualitative Health Research*, 15(9), 1277-1288.
Krippendorff, K. (2018). *Content Analysis: An Introduction to Its Methodology* (4ª ed.). Sage.
MacQueen, K.M., McLellan, E., Kay, K. e Milstein, B. (1998). Codebook development for team-based qualitative analysis. *Cultural Anthropology Methods*, 10(2), 31-36.
Mayring, P. (2014). *Qualitative Content Analysis: Theoretical Foundation, Basic Procedures and Software Solution*. Klagenfurt.
Miles, M.B., Huberman, A.M. e Saldaña, J. (2020). *Qualitative Data Analysis: A Methods Sourcebook* (4ª ed.). Sage.
Neuendorf, K.A. (2017). *The Content Analysis Guidebook* (2ª ed.). Sage.
Saldaña, J. (2021). *The Coding Manual for Qualitative Researchers* (4ª ed.). Sage.
Schreier, M. (2012). *Qualitative Content Analysis in Practice*. Sage.
Weber, R.P. (1990). *Basic Content Analysis* (2ª ed.). Sage.

**Confiabilidade**

Cohen, J. (1960). A coefficient of agreement for nominal scales. *Educational and Psychological Measurement*, 20(1), 37-46.
Krippendorff, K. (2004). Reliability in content analysis: some common misconceptions and recommendations. *Human Communication Research*, 30(3), 411-433.
Landis, J.R. e Koch, G.G. (1977). The measurement of observer agreement for categorical data. *Biometrics*, 33(1), 159-174.
Lombard, M., Snyder-Duch, J. e Bracken, C.C. (2002). Content analysis in mass communication: assessment and reporting of intercoder reliability. *Human Communication Research*, 28(4), 587-604.
Marzi, G., Balzano, M. e Marchiori, D. (2024). K-Alpha Calculator: Krippendorff's Alpha Calculator. *MethodsX*, 12, 102545.
O'Connor, C. e Joffe, H. (2020). Intercoder reliability in qualitative research. *International Journal of Qualitative Methods*, 19.

**Revisão de literatura e relato**

Booth, A., Sutton, A. e Papaioannou, D. (2016). *Systematic Approaches to a Successful Literature Review* (2ª ed.). Sage.
Breslin, D. e Gatrell, C. (2023). Theorizing through literature reviews: the miner-prospector continuum. *Organizational Research Methods*, 26(1), 139-167.
Denyer, D. e Tranfield, D. (2009). Producing a systematic review. Em Buchanan, D. e Bryman, A. (Orgs.), *The Sage Handbook of Organizational Research Methods*. Sage.
Gough, D., Oliver, S. e Thomas, J. (2017). *An Introduction to Systematic Reviews* (2ª ed.). Sage.
Kitchenham, B. e Charters, S. (2007). *Guidelines for Performing Systematic Literature Reviews in Software Engineering*. EBSE Technical Report.
Marzi, G., Balzano, M., Caputo, A. e Pellegrini, M.M. (2025). Guidelines for bibliometric-systematic literature reviews. *International Journal of Management Reviews*, 27(1), 81-103.
Okoli, C. (2015). A guide to conducting a standalone systematic literature review. *Communications of the Association for Information Systems*, 37, 879-910.
Page, M.J. et al. (2021a). The PRISMA 2020 statement: an updated guideline for reporting systematic reviews. *BMJ*, 372, n71.
Page, M.J. et al. (2021b). PRISMA 2020 explanation and elaboration. *BMJ*, 372, n160.
Paré, G., Trudel, M.-C., Jaana, M. e Kitsiou, S. (2015). Synthesizing information systems knowledge: a typology of literature reviews. *Information & Management*, 52(2), 183-199.
Pittaway, L., Robertson, M., Munir, K., Denyer, D. e Neely, A. (2004). Networking and innovation: a systematic review of the evidence. *International Journal of Management Reviews*, 5-6(3-4), 137-168.
Shea, B.J. et al. (2017). AMSTAR 2: a critical appraisal tool for systematic reviews. *BMJ*, 358, j4008.
Thomas, J. e Harden, A. (2008). Methods for the thematic synthesis of qualitative research in systematic reviews. *BMC Medical Research Methodology*, 8, 45.
Tranfield, D., Denyer, D. e Smart, P. (2003). Towards a methodology for developing evidence-informed management knowledge by means of systematic review. *British Journal of Management*, 14(3), 207-222.
Webster, J. e Watson, R.T. (2002). Analyzing the past to prepare for the future: writing a literature review. *MIS Quarterly*, 26(2), xiii-xxiii.
Whittemore, R. e Knafl, K. (2005). The integrative review: updated methodology. *Journal of Advanced Nursing*, 52(5), 546-553.
Wolfswinkel, J.F., Furtmueller, E. e Wilderom, C.P.M. (2013). Using grounded theory as a method for rigorously reviewing literature. *European Journal of Information Systems*, 22(1), 45-55.

**Síntese, teorização e uso de IA**

Duriau, V.J., Reger, R.K. e Pfarrer, M.D. (2007). A content analysis of the content analysis literature in organization studies. *Organizational Research Methods*, 10(1), 5-34.
Gatrell, C., Muzio, D., Post, C. e Wickert, C. (2024). Here, there and everywhere: on the responsible use of artificial intelligence (AI) in management research and the peer-review process. *Journal of Management Studies*, 61(3), 739-751.
Gioia, D.A., Corley, K.G. e Hamilton, A.L. (2013). Seeking qualitative rigor in inductive research: notes on the Gioia methodology. *Organizational Research Methods*, 16(1), 15-31.

**Verificação obrigatória**: antes de citar qualquer uma destas obras no manuscrito, confirme os dados bibliográficos na fonte. Não reproduza uma referência a partir deste arquivo sem checá-la.

---

## 16. PRINCÍPIO ORIENTADOR

A análise de conteúdo é replicável quando um terceiro, de posse do codebook, das regras e do corpus, chega às mesmas atribuições. Tudo neste protocolo serve a isso.

Duas consequências práticas. Quando não souber, pergunte ao usuário em vez de presumir: uma pergunta custa uma linha, uma suposição errada custa a recodificação do corpus. E quando um teste reprovar um procedimento, reporte a reprovação: um descarte documentado é evidência de rigor, e um descarte silencioso é o que a revisão por pares existe para encontrar.
