# Layout XML — NFC-e (modelo 65)

> 🚧 **Em construção.** Explica o que cada tag do XML da NFC-e (cupom) faz, para quem trabalha com webservice. Base: leiaute 4.00 do MOC e Notas Técnicas. Sempre confira com a NT vigente quando houver dúvida.
>
> **Dica:** use Ctrl+F com o nome da tag que veio na rejeição (ex.: `cEAN`).

A NFC-e usa **o mesmo leiaute de XML da NF-e**, por isso as rejeições citam `enviNFe/NFe/infNFe`. As diferenças estão nos valores permitidos e em algumas tags próprias (QR Code). Este arquivo traz a visão da NFC-e. O detalhe completo de cada grupo de imposto está em [NF-e (modelo 55)](NF-e%20(modelo%2055).md).

**Legenda — Obrig.:** S = obrigatória · N = opcional · C = condicional (depende de outra informação)


## Como ler o caminho que vem na rejeição

Exemplo: `Rejeição: Falha no Schema XML da NFe (Elemento: enviNFe/NFe[1]/infNFe/det[1]/prod/cEAN)`

| Parte | Significado |
|---|---|
| `enviNFe` | O lote enviado para a SEFAZ |
| `NFe[1]` | A 1ª nota dentro do lote |
| `infNFe` | Corpo da nota |
| `det[1]` | **Item 1** do cupom |
| `prod` | Bloco de dados do produto |
| `cEAN` | **A tag com problema** |

**"Falha no Schema XML"** quer dizer que a tag não segue o formato exigido. As causas mais comuns são:
• Tag vazia ou só com espaços.
• Espaço no início ou no fim do texto.
• Caractere inválido.
• Tamanho acima do máximo ou abaixo do mínimo.
• Número com vírgula, ou com casas decimais demais.
• Valor fora da lista permitida.

Caso real: [225 - Falha no Schema XML - cEAN inválido](../3%20-%20Retornos/NFC-e%20(modelo%2065)/225%20-%20Falha%20no%20Schema%20XML%20-%20cEAN%20inválido.md)


## Estrutura geral

```
enviNFe                 → lote
└── NFe                 → o cupom
    ├── infNFe          → conteúdo
    │   ├── ide         → identificação
    │   ├── emit        → emitente (a loja)
    │   ├── dest        → consumidor (opcional)
    │   ├── det         → itens
    │   │   ├── prod
    │   │   └── imposto
    │   ├── total
    │   ├── transp      → sempre "sem frete"
    │   ├── pag         → pagamento (obrigatório)
    │   ├── infAdic
    │   └── infRespTec
    ├── infNFeSupl      → QR Code e URL de consulta (só NFC-e)
    └── Signature
```


## O que muda em relação à NF-e

| Tag | Na NFC-e |
|---|---|
| `mod` | Sempre **65**. |
| `tpNF` | Sempre **1** (saída). |
| `idDest` | Sempre **1** (operação interna). |
| `finNFe` | **1** (normal). |
| `indFinal` | Sempre **1** (consumidor final). |
| `indPres` | **1** (presencial) ou **4** (entrega em domicílio). |
| `tpImp` | **4** = DANFE NFC-e impresso · **5** = DANFE NFC-e só em mensagem eletrônica. |
| `tpEmis` | **1** = normal · **9** = contingência offline (o cupom é emitido sem internet e enviado depois). |
| `dhSaiEnt` | Não é informada. |
| `dest` | Opcional. Quando informado, normalmente só o CPF/CNPJ. Endereço obrigatório na entrega em domicílio. |
| `CFOP` | Só CFOPs de venda a consumidor dentro do estado (ex.: 5101, 5102, 5405). CFOP fora da lista é rejeitado. |
| `modFrete` | Sempre **9** (sem frete). |
| `cobr` | Não é usado. |
| `pag` | Obrigatório, com o meio de pagamento real (dinheiro, cartão, PIX...). |
| `infNFeSupl` | Exclusivo da NFC-e: QR Code e URL de consulta. |


## ide — Identificação

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `cUF` | Código IBGE da UF do emitente. | 2 dígitos | S |
| `cNF` | Código aleatório que compõe a chave de acesso. | 8 dígitos | S |
| `natOp` | Natureza da operação (ex.: "VENDA"). | Texto 1–60 | S |
| `mod` | 65 = NFC-e. | 65 | S |
| `serie` | Série do cupom. | 0 a 999 | S |
| `nNF` | Número do cupom. | 1 a 999999999 | S |
| `dhEmi` | Data e hora de emissão, com fuso. Ex.: `2026-10-22T10:30:00-03:00`. | Data/hora UTC | S |
| `tpNF` | 1 = saída. | 1 | S |
| `idDest` | 1 = operação interna. | 1 | S |
| `cMunFG` | Código IBGE do município do emitente. | 7 dígitos | S |
| `tpImp` | 4 ou 5 (ver tabela acima). | 1 dígito | S |
| `tpEmis` | 1 = normal · 9 = contingência offline. | 1 dígito | S |
| `cDV` | Dígito verificador da chave de acesso. | 1 dígito | S |
| `tpAmb` | 1 = produção · 2 = homologação. | 1 ou 2 | S |
| `finNFe` | 1 = normal. | 1 | S |
| `indFinal` | 1 = consumidor final. | 1 | S |
| `indPres` | 1 = presencial · 4 = entrega em domicílio. | 1 dígito | S |
| `procEmi` | 0 = aplicativo do contribuinte. | 0 | S |
| `verProc` | Versão do sistema emissor. | Texto 1–20 | S |
| `dhCont` / `xJust` | Data/hora e justificativa da entrada em contingência (`tpEmis` = 9). | — | C |


## emit — Emitente

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CNPJ` | CNPJ da loja. | 14 dígitos | S |
| `xNome` / `xFant` | Razão social e nome fantasia. | Texto | S / N |
| `enderEmit` | Endereço: `xLgr`, `nro`, `xBairro`, `cMun`, `xMun`, `UF`, `CEP`... | — | S |
| `IE` | Inscrição estadual. | Até 14 | S |
| `CRT` | 1 = Simples Nacional · 2 = Simples com excesso de sublimite · 3 = Regime normal · 4 = MEI. Define se o item usa `CSOSN` ou `CST`. | 1 dígito | S |


## dest — Consumidor (opcional)

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CPF` / `CNPJ` / `idEstrangeiro` | Documento do consumidor ("CPF na nota"). | 11 / 14 dígitos | C |
| `xNome` | Nome do consumidor. | Texto 2–60 | N |
| `enderDest` | Endereço. Obrigatório quando `indPres` = 4. | — | C |
| `indIEDest` | 9 = não contribuinte. | 9 | C |


## det / prod — Produto

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `cProd` | **Código interno do produto** no sistema. | Texto 1–60 | S |
| `cEAN` | **Código de barras (GTIN)**: 8, 12, 13 ou 14 dígitos válidos, ou `SEM GTIN`. Não é o código interno. | GTIN ou `SEM GTIN` | S |
| `xProd` | Descrição do produto. Em homologação, o 1º item deve ter a descrição `NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL`. | Texto 1–120 | S |
| `NCM` | Classificação fiscal da mercadoria. | 8 dígitos | S |
| `CEST` | Código da Substituição Tributária, quando o produto tem ST. | 7 dígitos | C |
| `CFOP` | Código fiscal da operação (ex.: 5102 = venda; 5405 = venda com ST já retida). | 4 dígitos | S |
| `uCom` / `qCom` / `vUnCom` | Unidade, quantidade (até 4 casas) e valor unitário (até 10 casas). | — | S |
| `vProd` | Valor total bruto do item. | 2 casas decimais | S |
| `cEANTrib` | Código de barras da unidade tributável. Mesmas regras do `cEAN`. | GTIN ou `SEM GTIN` | S |
| `uTrib` / `qTrib` / `vUnTrib` | Unidade, quantidade e valor unitário tributáveis. | — | S |
| `vDesc` / `vOutro` | Desconto e outras despesas do item. | 2 casas decimais | N |
| `indTot` | 1 = entra no total do cupom. | 0 ou 1 | S |


## det / imposto — Impostos do item

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `vTotTrib` | Valor aproximado dos tributos (Lei 12.741/12), exibido no cupom. | 2 casas decimais | N |
| `orig` | Origem da mercadoria (0 = nacional...). | 0 a 8 | S |
| `CSOSN` | Situação tributária no Simples Nacional. Mais comuns no cupom: **102** (sem permissão de crédito) e **500** (ICMS já cobrado por ST). | 3 dígitos | C |
| `CST` (ICMS) | Situação tributária no regime normal. Mais comuns: **00** (tributado) e **60** (ICMS já cobrado por ST). | 2 dígitos | C |
| `vBC` / `pICMS` / `vICMS` | Base, alíquota e valor do ICMS (CST 00). | — | C |
| `vBCSTRet` / `pST` / `vICMSSTRet` | ST retida anteriormente (CST 60 / CSOSN 500). | — | C |
| `CST` (PIS/COFINS) | Situação do PIS e da COFINS (ex.: 01, 04, 06, 07, 49, 99). | 2 dígitos | S |
| `IBSCBS` | Grupo da Reforma Tributária (IBS e CBS). Ver detalhes na NF-e. | — | C |


## total / ICMSTot — Totais

Os totais precisam bater com a soma dos itens.

| Tag | O que é |
|---|---|
| `vProd` | Soma dos produtos. |
| `vDesc` | Soma dos descontos. |
| `vOutro` | Soma de outras despesas. |
| `vBC` / `vICMS` | Soma da base e do valor do ICMS. |
| `vPIS` / `vCOFINS` | Soma do PIS e da COFINS. |
| `vNF` | **Valor total do cupom.** Precisa ser igual à soma dos pagamentos menos o troco. |
| `vTotTrib` | Soma do valor aproximado dos tributos. |


## transp — Transporte

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `modFrete` | 9 = sem frete. | 9 | S |


## pag — Pagamento

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `detPag` | Uma forma de pagamento (pode repetir quando o cliente paga com mais de um meio). | — | S |
| `tPag` | 01 = dinheiro · 03 = cartão de crédito · 04 = cartão de débito · 05 = crédito loja · 10 = vale alimentação · 11 = vale refeição · 17 = PIX dinâmico · 18 = transferência / carteira digital · 20 = PIX estático · 99 = outros. | 2 dígitos | S |
| `xPag` | Descrição do meio. Obrigatório quando `tPag` = 99. | Texto 2–60 | C |
| `vPag` | Valor pago nesse meio. | 2 casas decimais | S |
| `card` → `tpIntegra` | 1 = integrado (TEF) · 2 = não integrado (POS). Obrigatório para cartão. | 1 ou 2 | C |
| `card` → `CNPJ` / `tBand` / `cAut` | CNPJ da credenciadora, bandeira e código de autorização. | — | N |
| `vTroco` | Troco devolvido ao cliente. | 2 casas decimais | N |


## infAdic — Informações adicionais

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `infCpl` | Mensagem complementar exibida no cupom. | Texto 1–5000 | N |


## infNFeSupl — QR Code (exclusivo da NFC-e)

Fica fora do `infNFe`, entre ele e a `Signature`.

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `qrCode` | Conteúdo do QR Code impresso no cupom: URL de consulta da SEFAZ + chave de acesso + parâmetros. Nas versões que exigem, inclui um hash gerado com o **CSC**. | Texto | S |
| `urlChave` | URL da SEFAZ para o consumidor consultar o cupom digitando a chave. | Texto | S |

**CSC (Código de Segurança do Contribuinte):** token gerado pela loja no portal da SEFAZ, junto com o **idCSC** (identificador). Os dois são configurados no sistema e usados para montar o QR Code. CSC errado ou vencido gera rejeição no QR Code.


## Retorno da SEFAZ

| Tag | O que é |
|---|---|
| `cStat` | **Código do resultado.** 100 = autorizado · 104 = lote processado · demais = rejeição (ver pasta `3 - Retornos`). |
| `xMotivo` | Descrição do resultado (mensagem da rejeição). |
| `chNFe` | Chave de acesso do cupom. |
| `nProt` | Número do protocolo de autorização. |
| `dhRecbto` | Data e hora do recebimento na SEFAZ. |
