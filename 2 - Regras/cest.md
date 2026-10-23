# CEST — Código Especificador da Substituição Tributária

O CEST identifica os bens e mercadorias passíveis de sujeição aos regimes de substituição tributária (ST) e de antecipação do ICMS. Ele uniformiza, entre as UFs, a lista de produtos que podem ter ST, e é informado no item da NF-e (modelo 55) e da NFC-e (modelo 65), logo abaixo do NCM.


## Fundamento legal

• Convênio ICMS 142/2018 — regra atual (vigente desde 01/01/2019). Os Anexos II a XXVI trazem os segmentos, itens, NCMs e CESTs.
• Convênio ICMS 92/2015 — regra anterior, que criou o CEST (revogado pelo 142/2018).
• NT 2015.003 e NT 2016.002 — inclusão do campo `CEST` e dos campos `indEscala` e `CNPJFab` no layout da NF-e/NFC-e.


## Formato do código

• 7 dígitos, no formato `SS.III.DD`:
  - `SS` — segmento (ex.: 01 = autopeças, 03 = cervejas, chopes, refrigerantes e águas, 21 = eletroeletrônicos);
  - `III` — item dentro do segmento;
  - `DD` — especificação do item.
• Exemplo: `01.015.00` (vidros automotivos).
• No XML vai **sem pontos**: `<CEST>0101500</CEST>`.
• A tag é opcional no schema (0–1 ocorrência por item) — a obrigatoriedade é definida pela regra de negócio, não pelo XSD.


## Quando informar

• Sempre que o produto estiver relacionado nos Anexos do Convênio ICMS 142/2018, **mesmo que a operação não tenha ST** (ex.: CST 00, ou produto que saiu da ST na UF). O CEST acompanha o produto, não a operação.
• Vale para todos os regimes: Regime Normal e Simples Nacional.
• Vale para NF-e e NFC-e.
• Obrigatório quando houver ICMS-ST destacado ou retido no item:
  - Regime Normal: CST 10, 30, 60, 70 e 90 (com ST);
  - Simples Nacional: CSOSN 201, 202, 203, 500 e 900 (com ST).
  - Sem CEST nesses casos, a SEFAZ rejeita a nota (**Rejeição 806 — Operação com ICMS-ST sem informação do CEST**).


## Quando NÃO informar

• Produto que não está em nenhum Anexo do Convênio ICMS 142/2018: a tag `CEST` deve ser omitida (não enviar vazia, nem com zeros).
• Não "inventar" CEST por semelhança: se o NCM do produto não aparece no Anexo, não há CEST.


## Correlação NCM × CEST

• Cada CEST está vinculado a um ou mais NCMs (ou posições/subposições de NCM) no Anexo do convênio.
• O CEST informado precisa corresponder ao NCM do item. Algumas UFs validam essa correlação na autorização e rejeitam a nota quando não batem.
• Quando o Anexo lista o NCM por posição (4 dígitos) ou subposição (6 dígitos), todos os NCMs de 8 dígitos dentro dela entram — desde que a descrição do produto também corresponda à descrição do CEST.
• Um mesmo NCM pode ter mais de um CEST possível; nesse caso, o que define é a **descrição** do produto no Anexo.


## Escala industrial não relevante (`indEscala` e `CNPJFab`)

Alguns itens (Anexo XXVII do Convênio ICMS 142/2018) não se sujeitam à ST quando fabricados em escala industrial não relevante (fabricante optante pelo Simples Nacional que atende aos requisitos do convênio).

| Campo | Descrição | Regra |
|---|---|---|
| `indEscala` | Indicador de escala relevante. `S` = produzido em escala relevante · `N` = produzido em escala **não** relevante. | Informar junto com o CEST quando o item se enquadrar na regra de escala. |
| `CNPJFab` | CNPJ do fabricante da mercadoria. | Obrigatório quando `indEscala = N`. |

• Quem emite como fabricante em escala não relevante deve informar `indEscala = N` e o próprio CNPJ em `CNPJFab`.
• Na revenda do produto, os mesmos dados do fabricante devem ser repassados.


## Ordem das tags no XML (grupo `prod`)

```xml
<NCM>70072100</NCM>
<CEST>0101500</CEST>
<indEscala>S</indEscala>       <!-- quando aplicável -->
<CNPJFab>00000000000000</CNPJFab> <!-- só quando indEscala = N -->
<cBenef>...</cBenef>           <!-- quando a UF exige -->
<CFOP>5405</CFOP>
```


## Regras operacionais para o cadastro

• O CEST deve ficar no **cadastro do produto**, junto com o NCM — não deve ser escolhido na hora da emissão.
• Ao alterar o NCM de um produto, revisar o CEST (pode deixar de existir ou mudar).
• Quando uma UF retira um produto da ST (ex.: SP com autopeças em 2026), o CEST **continua** sendo informado na nota. Ver [regra_icms_st_sp_autopecas.md](../reforma_tributaria/regra_icms_st_sp_autopecas.md).
• Acompanhar as alterações do Convênio ICMS 142/2018 (os Anexos são atualizados com frequência por novos convênios).
• Erro de CEST em nota já autorizada: em regra é corrigível por CC-e, por não alterar base de cálculo, alíquota nem valor do imposto — confirmar com a contabilidade quando o erro mudar o enquadramento na ST. Ver [carta-de-correção.md](carta-de-correção.md).
