# Tributação monofásica de PIS/COFINS: guia para suporte fiscal (foco em autopeças)

> Elaborado em 10/11/2026. Os exemplos numéricos são **ilustrativos**; confirme NCM, alíquotas e legislação vigente antes de orientar um caso real.

---

## Em uma frase

**NCM enquadrado + emitente revendedor = CST 04, grupo `PISNT`/`COFINSNT`, sem base de cálculo, alíquota ou valor.**

- **O produto monofásico se identifica pelo NCM.** Para autopeças, a lista de NCMs está nos Anexos I e II da Lei 10.485/02, e a Tabela 4.3.10 traz as alíquotas concentradas.
- **O tributo já foi pago no topo da cadeia**, pelo fabricante ou importador, com alíquota concentrada (CST 02, ou 01).
- **O revendedor não recolhe PIS/COFINS na venda** porque a lei fixa alíquota zero. O CST 04 é como ele informa isso na nota, e só vale se o NCM estiver mesmo enquadrado.

---

## 1. O que é tributação monofásica

Tributação monofásica é a cobrança de um tributo **uma única vez na cadeia**, em geral pelo fabricante ou importador, com **alíquota maior (concentrada)**. Nas revendas seguintes (atacado e varejo), a receita fica com **alíquota zero**.

Hoje ela existe:

- **No PIS/COFINS** de autopeças, pneus, veículos, medicamentos, perfumaria e higiene, bebidas frias e combustíveis (Leis 10.147/2000 e 10.485/2002, entre outras).
- **No ICMS sobre combustíveis** (LC 192/2022). É outro tributo, com outra lei: um produto pode ser monofásico nos dois sistemas ao mesmo tempo, cada um com suas regras.

**No Simples Nacional**, a empresa que revende esses produtos **segrega a receita no PGDAS-D** para não pagar PIS e COFINS de novo dentro do DAS.

---

## 2. Como funciona: alíquota concentrada e exemplo numérico

### Alíquota concentrada
É a alíquota mais alta que o fabricante ou importador paga **sozinho**, no lugar de toda a cadeia.

- **Regime normal (não cumulativo):** cada elo paga uma alíquota menor sobre a sua venda (por exemplo, 1,65% + 7,6%) e desconta o crédito da etapa anterior.
- **Monofásico:** a lei concentra tudo na primeira etapa. O fabricante ou importador paga uma alíquota maior, que já embute o que seria recolhido pelos elos seguintes. Distribuidor e varejista vendem a alíquota zero.

Exemplo conceitual: no regime normal, fábrica paga X, distribuidor paga Y e oficina paga Z. No monofásico, a fábrica paga uma alíquota concentrada equivalente a X+Y+Z, e os demais pagam zero.

### Exemplo numérico simplificado: o que o fabricante/importador paga

Pneu (NCM 40.11), alíquotas do código 304 da Tabela 4.3.10: PIS 2,00% + COFINS 9,50% = **11,50%**.

Venda do importador a R$ 120,00 → PIS/COFINS concentrado = 120,00 × 11,50% = **R$ 13,80**.

O revendedor que compra esse pneu e revende a R$ 150,00 **não recolhe PIS/COFINS** sobre a venda (CST 04).

---

## 3. Como decidir se um produto é monofásico: a Tabela 4.3.10 da EFD-Contribuições

O documento de referência é a **Tabela 4.3.10 da EFD-Contribuições** (versão 1.25, atualizada em 30/03/2026): "Produtos sujeitos a alíquotas diferenciadas: incidência monofásica e por pauta (bebidas frias), CST 02 e 04".

### Grupos da tabela

| Grupo | Conteúdo |
|---|---|
| 100 | Combustíveis e álcool |
| 200 | Fármacos e perfumarias |
| 300 | Veículos, máquinas e autopeças |
| 400 | Bebidas frias |

### Linhas relevantes para autopeças e pneus (grupo 300)

| Código | Descrição | NCM | PIS % | COFINS % |
|---|---|---|---|---|
| 301 | Veículos automotores e máquinas agrícolas | Posições listadas (87.01 a 87.06, 84.29 etc.) | 2,00 | 9,60 |
| 302 | Autopeças, vendas para atacadistas, varejistas e consumidores | Anexos I e II da Lei 10.485/02 | 2,30 | 10,80 |
| 303 | Autopeças, vendas para fabricantes de veículos, máquinas e autopeças | Anexos I e II da Lei 10.485/02 | 1,65 | 7,60 |
| 304 | Pneumáticos (pneus novos e câmaras de ar) | 40.11 e 40.13 | 2,00 | 9,50 |
| 003 / 399 | Revenda de veículos, máquinas e autopeças | (sem NCM) | 0,00 | 0,00 |

### Roteiro de decisão

1. **Pegar o NCM** do item (na nota rejeitada ou no cadastro do produto).
2. **Conferir se o NCM está enquadrado:** para autopeças, nos Anexos I e II da Lei 10.485/02; para pneus, 40.11 e 40.13.
3. **Identificar o perfil do emitente:** revendedor ou fabricante/importador.
4. **Aplicar o CST correspondente** (seção 4).

### Limites do documento

- Para autopeças, a coluna de NCM só diz "Anexos I e II da Lei nº 10.485/02". **A lista de NCMs está na lei, não na tabela.**
- A observação I da própria tabela avisa que a **ausência de um NCM na tabela não significa** que ele não possa ter o tratamento monofásico. Por isso, a tabela sozinha não prova nem descarta o enquadramento.
- A observação II define a regra da revenda: no caso de comercialização com **CST 04**, considera-se alíquota zero quando a pessoa jurídica **não** é fabricante, industrial, importador ou equiparado.

---

## 4. Qual CST usar

### Quadro por perfil

| Perfil do emitente | CST PIS/COFINS | Grupo no XML | Observação |
|---|---|---|---|
| **Revendedor** de produto monofásico | **04** | `PISNT` / `COFINSNT` | Revenda a alíquota zero |
| **Fabricante/importador**, alíquota concentrada (percentual) | **02** (ou 01, conforme o caso) | `PISAliq` / `COFINSAliq` | Tabela 4.3.10 |
| **Fabricante/importador**, alíquota por unidade de medida | **03** | `PISQtde` / `COFINSQtde` | Tabela 4.3.11 |
| Produto **não** monofásico, regime normal | 01 | `PISAliq` / `COFINSAliq` | Alíquota cheia do regime |

### CST 04 com "alíquota zero": a pegadinha do XML

CST 04 significa "operação tributável monofásica, revenda a alíquota zero". A alíquota é zero **por definição do CST**, então **não se informa alíquota 0 no XML**. O grupo usado é o de não tributado, que leva só o CST:

```xml
<PIS>
  <PISNT>
    <CST>04</CST>
  </PISNT>
</PIS>
<COFINS>
  <COFINSNT>
    <CST>04</CST>
  </COFINSNT>
</COFINS>
```

- Enviar `PISAliq` com `pPIS=0,00` e CST 04 costuma gerar **rejeição de schema**, porque o CST não pertence a esse grupo.
- Enviar `vBC`, `pPIS` ou `vPIS` dentro de `PISNT` também é inválido.

### CST 04 x CST 06: a diferença

Os dois CSTs são de **PIS/COFINS** e resultam em "nada a recolher" naquela venda, mas por motivos diferentes.

| | **CST 04** | **CST 06** |
|---|---|---|
| Tributo | PIS/COFINS | PIS/COFINS |
| Nome | Operação tributável monofásica, **revenda a alíquota zero** | Operação tributável a **alíquota zero** |
| Por que não há tributo | O tributo **já foi pago** na etapa concentrada (fabricante/importador) | A lei **desonera** a operação (ex.: cesta básica) |
| Origem da regra | Tabelas 4.3.10 e 4.3.11 | Tabela 4.3.13 |
| Quem usa | Revendedor de produto monofásico | Quem vende produto com alíquota zero por determinação legal |
| Grupo no XML | `PISNT` / `COFINSNT` | `PISNT` / `COFINSNT` |
| Risco de confundir | Usar 06 em item monofásico descaracteriza o enquadramento e some a rastreabilidade do monofásico | Usar 04 em item não monofásico declara um tributo "já pago" que não foi |

Resumo: **CST 04 = o imposto existe, mas foi pago antes. CST 06 = o imposto não existe naquela operação.**

(Outros CSTs próximos de PIS/COFINS: 05 é substituição tributária de PIS/COFINS, e 49 costuma ser usado de forma informativa por emitentes do Simples. Confirme a parametrização do ERP.)

### O que cada CST significa

| CST | Tributo | Significado |
|---|---|---|
| 60 | ICMS | ICMS já cobrado antes, por substituição tributária |
| 04 | PIS/COFINS | Monofásico: revenda com alíquota zero |
| 06 | PIS/COFINS | Alíquota zero (por outro motivo legal, não monofásico) |

O CST 60 é de **ICMS**, e não de PIS/COFINS, então não se compara com o CST 04. Ele não quer dizer "alíquota zero": quer dizer que o ICMS já foi recolhido antes, por ST. A nota tem um CST de cada tributo, e uma rejeição de ICMS (por exemplo, CFOP 5405 sem CST 60 ou CSOSN 500) não se resolve trocando o CST de PIS/COFINS.

---

## 5. Exemplo prático: NCM 40.11 (pneus) e o erro do ERP

Cadeia: importadora → revendedor → oficina. Valores hipotéticos; ignora II, IPI, ICMS e créditos.

### 5.1 Importadora (paga a alíquota concentrada)

Preço planejado só com custo de entrada:

| Item | R$ por unidade |
|---|---|
| Mercadoria | 70,00 |
| Frete | 10,00 |
| Despesas aduaneiras | 5,00 |
| **Custo considerado** | **85,00** |
| Preço de venda planejado | 120,00 |
| **Margem prevista** | **35,00 (29,2%)** |

Realidade: PIS/COFINS concentrado na venda = 120,00 × 11,50% = **R$ 13,80**. Margem real = 35,00 − 13,80 = **R$ 21,20 (17,7%)**. A margem cai quase 40% por não considerar o tributo.

**Lição:** o NCM precisa ser analisado **antes da nacionalização**. Produtos parecidos podem ter tratamentos diferentes conforme a classificação fiscal.

### 5.2 Revendedor (regime normal)

Compra por R$ 120,00 e revende a R$ 150,00.

| Cenário | PIS/COFINS na venda | Margem |
|---|---|---|
| **Correto (CST 04)** | 0,00 | **30,00 (20,0%)** |
| **Erro do ERP: tratou como produto normal** (CST 01, 1,65% + 7,60% = 9,25%) | 150,00 × 9,25% ≈ 13,88 | ≈ **16,12 (10,7%)** |

O cliente paga imposto que não devia, em duplicidade com a importadora. Pode pedir restituição ou compensação, mas até lá vira prejuízo recorrente.

### 5.3 O erro inverso

CST 04 em produto cujo NCM **não** é monofásico: a nota passa na SEFAZ, mas o cliente deixa de recolher tributo devido. Risco de autuação, com multa e juros.

### 5.4 Erros mais comuns no atendimento

1. CST 04 com grupo errado (`PISAliq` ou `PISOutr`) → rejeição de schema (falha de parametrização do ERP).
2. NCM cadastrado errado ou genérico → enquadramento incorreto (erro de cadastro do cliente).
3. CST 01 em produto monofásico → a nota passa, mas o cliente paga a mais.
4. CST 04 em produto não monofásico → a nota passa, mas há subdeclaração de tributo.
5. Fabricante ou importador usando CST 04 → eles são o contribuinte da etapa concentrada e usam CST 02 (ou 01).
6. CFOP de ST (5405) sem CST de ICMS 60 / CSOSN 500 (ou o inverso) → rejeição de ICMS, sem relação com PIS/COFINS.

### 5.5 Como separar falha do ERP de erro do cliente

| Sintoma | Causa provável | De quem é |
|---|---|---|
| Rejeição de schema no grupo PIS/COFINS com CST 04 | Grupo errado no XML | ERP |
| Rejeição ou imposto incorreto com NCM fora da lista | NCM errado no cadastro | Cliente |
| Nota autorizada, mas o cliente reclama de imposto alto | CST 01 aplicado a item monofásico (regra ou cadastro) | ERP ou cliente, conforme a parametrização |
| Nota autorizada, cliente do Simples reclama do DAS | Receita não segregada no PGDAS-D | Cliente / contador |

---

## 6. Simples Nacional

No Simples, o PIS/COFINS está **embutido no DAS**. O revendedor de produto monofásico pode (e deve) **segregar essa receita no PGDAS-D**, excluindo a parcela de PIS/COFINS do cálculo, porque o tributo já foi pago pelo fabricante ou importador (art. 18, § 4º-A, da LC 123/2006). Se não segrega, paga duas vezes.

### Exemplo ilustrativo (revendedor de pneus, Anexo I)

Premissas: PIS+COFINS ≈ 15,5% do DAS na 1ª faixa do Anexo I e alíquota efetiva de 4%. Confira a tabela vigente e a alíquota efetiva real do cliente.

| Item | Sem segregar (errado) | Segregando (correto) |
|---|---|---|
| Venda do pneu | 150,00 | 150,00 |
| DAS (4%) | 6,00 | 6,00 |
| Parcela de PIS/COFINS no DAS | 0,93 | excluída |
| **DAS devido** | **6,00** | **5,07** |
| Custo de compra | 120,00 | 120,00 |
| **Margem** | **24,00** | **24,93** |

A diferença por unidade é pequena, mas em distribuidoras de autopeças, onde grande parte do faturamento é monofásica, vira valor relevante no ano.

### Pontos de atenção

- O ICMS segue as regras do Simples (CSOSN 101, 102, 500 etc.) e não muda por causa do monofásico.
- O grupo de PIS/COFINS na nota do optante do Simples costuma ser **informativo**. **O que determina o imposto é a declaração no PGDAS-D**, e não o CST da nota.
- Fabricante ou importador optante do Simples, em regra, não segrega: a segregação vale para a **revenda**. Confirmar com o contador.
- Receitas de ICMS-ST têm segregação própria; não confundir com a do monofásico.
- **Oportunidade para o ERP:** relatório de vendas por NCM ou por CST, que o contador usa para segregar. Se não existe, é melhoria de produto.

---

## 7. Reforma Tributária (CBS substitui PIS/COFINS)

### O essencial

Com a LC 214/2025, o PIS e a COFINS são **extintos em 2027** e substituídos pela **CBS**, que incide em todas as etapas da cadeia, com direito a crédito. Os regimes monofásicos de PIS/COFINS, incluindo o de autopeças, **deixam de existir** (segundo as fontes consultadas, a extinção estaria no art. 109 da LC 214/2025; confirmar no texto da lei). Fica uma lógica de concentração para combustíveis, com regime próprio.

O raciocínio das seções anteriores (importador paga tudo; revendedor sai com CST 04) vale **até 31/12/2026**.

### Cronograma

| Período | O que acontece |
|---|---|
| **2026** | Teste: CBS 0,9% + IBS 0,1%, compensáveis. Monofásico atual vale integralmente. |
| **2027** | CBS substitui PIS/COFINS, com alíquota padrão estimada em **8,8%**. IBS com alíquota de transição de 0,1% em 2027 e 2028. |
| **2029 a 2032** | IBS entra gradualmente, junto com a transição do ISS e do ICMS. |

**Atenção:** a alíquota de referência ainda será definida pelo Senado; vale provisoriamente o cálculo do TCU. Trate 8,8% como estimativa.

### Exemplo (pneu, ilustrativo)

Mesmos R$ 120,00 de compra e R$ 150,00 de venda, CBS de 8,8%, sem ajuste de preços e sem IBS.

| | Hoje (monofásico) | 2027 (CBS) |
|---|---|---|
| Tributo na venda do revendedor | 0,00 (CST 04) | 150 × 8,8% = **13,20** (débito) |
| Crédito sobre a compra | não há | 120 × 8,8% = **10,56** |
| **Recolhimento líquido** | **0,00** | **2,64** |

O revendedor passa a recolher CBS, mas só sobre o valor agregado (30 × 8,8% = 2,64), porque abate o crédito da compra.

### Crédito presumido sobre estoque

Empresas que operavam em regime monofásico ou ST até o fim de 2026 poderão apurar **crédito presumido da CBS sobre os estoques** mantidos em 1º/01/2027. Para distribuidores de autopeças, com muito estoque, é um ponto que o ERP e o contador precisam tratar antes da virada.

### Simples Nacional e a competitividade em vendas B2B

Este é o ponto de maior impacto para o setor de autopeças, onde predomina a venda B2B.

- O Simples continua existindo, e o DAS passa a incluir a CBS no lugar do PIS/COFINS dentro do anexo.
- A opção pelo **regime regular de IBS e CBS** não é obrigatória; quem não escolher continua, no primeiro semestre de 2027, com IBS e CBS dentro do recolhimento unificado.
- **A lógica competitiva:** hoje, o monofásico dá ao revendedor do Simples uma carga de PIS/COFINS próxima de zero. Em 2027, o comprador do regime regular (Lucro Presumido ou Real) **só aproveita crédito conforme o que o fornecedor recolhe**. Comprar de um fornecedor que fica no DAS tende a gerar menos crédito do que comprar de um fornecedor no regime regular. Isso muda preços e negociações entre empresas, e pode fazer o fornecedor do Simples perder competitividade em vendas B2B, ou levá-lo a considerar o regime regular de IBS e CBS.
- A escolha do modelo de recolhimento influencia custos, preços e negociações. O Simples deve simular os dois cenários com faturamento, compras e perfil de clientes reais (a opção tem prazo; confirmar a data vigente).
- Para optantes do Simples, a NFS-e padrão nacional já é obrigatória em novembro de 2026 e as regras de IBS/CBS produzem efeitos a partir de janeiro de 2027.

### Impacto para o ERP e para o suporte

- Os CSTs de PIS/COFINS (04, 02 etc.) saem de cena em 2027 e entram os **CST de IBS/CBS** e o **cClassTrib** no leiaute.
- Espere uma onda de **rejeições** por grupos IBS/CBS ausentes ou com CST/cClassTrib incorreto, especialmente em clientes que hoje usam CST 04.
- Os XMLs de exemplo do projeto (NF-e e NFS-e da Reforma Tributária 1.0) são a base para validar quais grupos novos o ERP precisa preencher.
- Relatório de estoque na virada de 2026 para 2027, para apoiar o crédito presumido.

---

## 8. Checklist rápido para investigar uma rejeição ou reclamação

1. **Qual o perfil do emitente?** Revendedor, fabricante, importador, Simples ou regime normal?
2. **Qual o NCM do item?** Consta nos Anexos I/II da Lei 10.485/02 (ou 40.11 e 40.13)?
3. **Qual CST foi enviado?** O correto seria 04 (revenda), 02/03 (fabricante/importador) ou 01 (não monofásico)?
4. **Qual grupo do XML foi usado?** CST 04 exige `PISNT`/`COFINSNT`, só com o CST.
5. **A rejeição é de PIS/COFINS ou de ICMS?** (CFOP 5405 x CST 60 / CSOSN 500 são regras de ICMS.)
6. **O cliente é do Simples?** Se a reclamação for de imposto e não de rejeição, verificar a segregação no PGDAS-D.
7. **A data é a partir de 2027?** Se sim, o monofásico acabou e as regras são de IBS/CBS.
8. **Falha do ERP ou erro do cliente?** Usar o quadro da seção 5.5.

---

## 9. Veja também

- [[cest]]: CEST e correlação com o NCM.
- [[regra_icms_st_sp_autopecas]]: saída das autopeças e pneus da ST de ICMS em SP (o ICMS-ST é um assunto separado do monofásico de PIS/COFINS).
- [[NF-e (modelo 55)]]: layout dos grupos de PIS/COFINS no XML.

---

## 10. Fontes

- Tabela 4.3.10 da EFD-Contribuições, versão 1.25 (atualizada em 30/03/2026), arquivo `TABELA_1.DOC` do Google Drive.
- [Reforma Tributária e o setor de autopeças B2B (Contábeis)](https://www.contabeis.com.br/artigos/71953/nova-lei-tributaria-impacta-setor-de-autopecas-entenda-a-cbs/)
- [Produtos Monofásicos de PIS e COFINS: Guia Completo](https://blog.esimplesauditoria.com.br/quais-os-tipos-de-produtos-sujeitos-a-tributacao-monofasica/)
- [Extinção do PIS/Cofins e entrada da CBS (Jornal Contábil)](https://jornalcontabil.com.br/noticia/extincao-do-pis-cofins-e-entrada-da-cbs-exigem-atencao-das-empresas/)
- [Simples Nacional: crédito de impostos muda em 2027 (Jornal Contábil)](https://jornalcontabil.com.br/noticia/simples-nacional-credito-de-impostos-muda-em-2027/)
- [Quanto custa ser PJ em 2027 (Meu Contador Online)](https://www.meucontadoronline.com.br/blog/quanto-custa-ser-pj-em-2027/)
- [Reforma Tributária 2027 (Contabilivre)](https://www.contabilivre.com.br/blog/reforma-tributaria-2027-o-que-muda-para-empresas/)
- [Alíquota da CBS (Guia Tributário)](https://guiatributario.net/tag/regime-monofasico/)
- [PIS/COFINS monofásico: guia por NCM (NCM Buscador)](https://buscadorncm.com.br/blog/pis-cofins-monofasico-guia-por-ncm)

**Ressalva:** as fontes sobre a Reforma Tributária são majoritariamente blogs e portais de contabilidade, e não o texto da lei. A alíquota da CBS, as regras de crédito presumido e o tratamento do Simples podem mudar por regulamentação. Confirmar na LC 214/2025 e nas notas técnicas da NF-e antes de orientar clientes.
