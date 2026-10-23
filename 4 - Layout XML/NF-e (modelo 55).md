# Layout XML — NF-e (modelo 55)

> 🚧 **Em construção.** Explica o que cada tag do XML da NF-e faz, para quem trabalha com webservice. Base: leiaute 4.00 do Manual de Orientação do Contribuinte (MOC) e Notas Técnicas. Sempre confira com a NT vigente quando houver dúvida.
>
> **Dica:** use Ctrl+F com o nome da tag que veio na rejeição (ex.: `cProd`).

**Legenda — Obrig.:** S = obrigatória · N = opcional · C = condicional (depende de outra informação)


## Como ler o caminho que vem na rejeição

Exemplo: `Rejeição: Falha no Schema XML da NFe (Elemento: enviNFe/NFe[1]/infNFe/det[1]/prod/cEAN)`

| Parte | Significado |
|---|---|
| `enviNFe` | O lote enviado para a SEFAZ |
| `NFe[1]` | A 1ª nota dentro do lote |
| `infNFe` | Corpo da nota |
| `det[1]` | **Item 1** da nota (o número entre colchetes é a posição do item) |
| `prod` | Bloco de dados do produto |
| `cEAN` | **A tag com problema** |

**"Falha no Schema XML"** quer dizer que a tag não segue o formato exigido. As causas mais comuns são:
• Tag vazia (`<cProd></cProd>`) ou só com espaços.
• Espaço no início ou no fim do texto.
• Caractere inválido (quebra de linha, tabulação, alguns símbolos).
• Texto maior que o tamanho máximo, ou menor que o mínimo.
• Número com vírgula no lugar do ponto, com separador de milhar, ou com casas decimais demais.
• Valor fora da lista permitida (ex.: `tpNF` = 5).
• Tags fora da ordem definida no leiaute.

**Formato de números:** sempre com ponto decimal e sem separador de milhar. Ex.: `1500.75`.
**Formato de data/hora:** `AAAA-MM-DDThh:mm:ss-03:00`. Ex.: `2026-10-22T10:30:00-03:00`.


## Estrutura geral

```
enviNFe                 → lote
└── NFe                 → a nota
    ├── infNFe          → conteúdo da nota
    │   ├── ide         → identificação da nota
    │   ├── emit        → emitente
    │   ├── dest        → destinatário
    │   ├── det         → itens (um por produto)
    │   │   ├── prod    → dados do produto
    │   │   └── imposto → impostos do item
    │   ├── total       → totais da nota
    │   ├── transp      → transporte
    │   ├── cobr        → fatura / duplicatas
    │   ├── pag         → pagamento
    │   ├── infAdic     → informações adicionais
    │   └── infRespTec  → responsável técnico (software house)
    └── Signature       → assinatura digital
```


## Lote e raiz

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `enviNFe` | Lote enviado. Atributo `versao="4.00"`. | — | S |
| `idLote` | Número do lote, gerado pelo sistema. | Até 15 dígitos | S |
| `indSinc` | Processamento: 0 = assíncrono (consulta depois pelo recibo) · 1 = síncrono (resposta na hora). | 0 ou 1 | S |
| `NFe` | Uma nota fiscal dentro do lote. | — | S |
| `infNFe` | Conteúdo da nota. Atributo `Id` = "NFe" + chave de acesso (44 dígitos). | — | S |
| `Signature` | Assinatura digital feita com o certificado do emitente. Se o XML for alterado depois de assinado, a assinatura fica inválida. | — | S |


## ide — Identificação da nota

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `cUF` | Código IBGE da UF do emitente (ex.: 35 = SP, 22 = PI). | 2 dígitos | S |
| `cNF` | Código numérico aleatório que compõe a chave de acesso. Não pode ser igual ao `nNF`. | 8 dígitos | S |
| `natOp` | Natureza da operação, por extenso (ex.: "VENDA DE MERCADORIA"). | Texto 1–60 | S |
| `mod` | Modelo do documento: **55** = NF-e · **65** = NFC-e. | 55 ou 65 | S |
| `serie` | Série da nota. | 0 a 999 | S |
| `nNF` | Número da nota. | 1 a 999999999 | S |
| `dhEmi` | Data e hora de emissão, com fuso. | Data/hora UTC | S |
| `dhSaiEnt` | Data e hora da saída ou entrada da mercadoria. | Data/hora UTC | N |
| `tpNF` | Tipo: 0 = entrada · 1 = saída. | 0 ou 1 | S |
| `idDest` | Destino: 1 = interna (mesma UF) · 2 = interestadual · 3 = exterior. Precisa combinar com o CFOP (5xxx, 6xxx ou 7xxx). | 1, 2 ou 3 | S |
| `cMunFG` | Código IBGE do município onde ocorre o fato gerador. | 7 dígitos | S |
| `tpImp` | Formato do DANFE: 1 = retrato · 2 = paisagem · 3 = simplificado. | 0 a 5 | S |
| `tpEmis` | Forma de emissão: 1 = normal · 6 = contingência SVC-AN · 7 = contingência SVC-RS (entre outras). | 1 dígito | S |
| `cDV` | Dígito verificador da chave de acesso (último dígito da chave). | 1 dígito | S |
| `tpAmb` | Ambiente: 1 = produção · 2 = homologação (teste). | 1 ou 2 | S |
| `finNFe` | Finalidade: 1 = normal · 2 = complementar · 3 = ajuste · 4 = devolução. | 1 a 4 | S |
| `indFinal` | 0 = operação normal · 1 = consumidor final. | 0 ou 1 | S |
| `indPres` | Presença do comprador: 0 = não se aplica · 1 = presencial · 2 = internet · 3 = teleatendimento · 4 = entrega em domicílio (NFC-e) · 5 = presencial fora do estabelecimento · 9 = outros. | 1 dígito | S |
| `indIntermed` | Venda por plataforma de terceiros (marketplace): 0 = não · 1 = sim. | 0 ou 1 | C |
| `procEmi` | Processo de emissão: 0 = aplicativo do contribuinte (nosso sistema). | 0 a 3 | S |
| `verProc` | Versão do sistema que gerou a nota. | Texto 1–20 | S |
| `NFref` / `refNFe` | Chave da nota referenciada. Usada em devolução, complementar e ajuste. | 44 dígitos | C |


## emit — Emitente

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CNPJ` / `CPF` | Documento do emitente, só números. | 14 / 11 dígitos | S |
| `xNome` | Razão social. | Texto 2–60 | S |
| `xFant` | Nome fantasia. | Texto 1–60 | N |
| `enderEmit` | Bloco de endereço (tags abaixo). | — | S |
| `xLgr` | Logradouro. | Texto 2–60 | S |
| `nro` | Número. Sem número: `SN` ou `0`. | Texto 1–60 | S |
| `xCpl` | Complemento. **Máximo 60 caracteres** — acima disso a nota cai em Falha no Schema XML (225). | Texto 1–60 | N |
| `xBairro` | Bairro. | Texto 2–60 | S |
| `cMun` / `xMun` | Código IBGE (7 dígitos) e nome do município. | — | S |
| `UF` | Sigla da UF. | 2 letras | S |
| `CEP` | CEP, só números. | 8 dígitos | N |
| `cPais` / `xPais` | País: 1058 / BRASIL. | — | N |
| `fone` | Telefone, só números. | 6–14 dígitos | N |
| `IE` | Inscrição estadual, só números. | Até 14 | S |
| `IEST` | IE do substituto tributário na UF de destino. | Até 14 | C |
| `IM` / `CNAE` | Inscrição municipal e CNAE. Só quando a nota tem serviço junto. | — | C |
| `CRT` | Regime tributário: 1 = Simples Nacional · 2 = Simples Nacional com excesso de sublimite · 3 = Regime normal · 4 = MEI. **Define se o item usa `CSOSN` (Simples) ou `CST` (normal).** | 1 dígito | S |


## dest — Destinatário

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CNPJ` / `CPF` / `idEstrangeiro` | Documento do destinatário. | 14 / 11 dígitos | S |
| `xNome` | Nome ou razão social. Em homologação deve ser `NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL`. | Texto 2–60 | S |
| `enderDest` | Endereço (mesmas tags do `enderEmit`). | — | S |
| `indIEDest` | 1 = contribuinte do ICMS (tem IE) · 2 = contribuinte isento · 9 = não contribuinte. | 1, 2 ou 9 | S |
| `IE` | IE do destinatário. Obrigatória quando `indIEDest` = 1. | Até 14 | C |
| `email` | E-mail para envio do XML/DANFE. | Texto 1–60 | N |

> **Limite do `xCpl` (vale para `enderEmit` e `enderDest`):** no máximo 60 caracteres, contando os espaços. O sistema não deve cortar o texto sozinho, porque pode perder informação. O certo é abreviar no cadastro do cliente.
>
> Exemplo real (65 caracteres, rejeitado):
> `<xCpl>LOTE 420/430/440 EDIF CITY OFFICES ANDAR 2 SALA 243 A 248 PARTE A</xCpl>`
>
> Abreviado (52 caracteres, aceito):
> `<xCpl>LT 420/430/440 ED CITY OFFICES AND 2 SL 243-248 PT A</xCpl>`
>
> Se mesmo abreviado não couber, parte do endereço pode ir para `xLgr` (ex.: `SIG QUADRA 2 LOTE 420/430/440`), que também aceita até 60 caracteres.


## det / prod — Produto (um bloco por item)

O `det` tem o atributo `nItem` (1 a 990), que é o número do item. É ele que aparece como `det[1]`, `det[2]`... na rejeição.

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `cProd` | **Código interno do produto** no sistema do emitente. Sem código próprio (itens que não são mercadoria): usar "CFOP" + número, ex.: `CFOP5102`. | Texto 1–60 | S |
| `cEAN` | **Código de barras (GTIN)** do produto: 8, 12, 13 ou 14 dígitos, com dígito verificador válido. Sem código de barras: `SEM GTIN`. Não é o código interno. | GTIN ou `SEM GTIN` | S |
| `xProd` | Descrição do produto. | Texto 1–120 | S |
| `NCM` | Classificação fiscal da mercadoria (Nomenclatura Comum do Mercosul). | 8 dígitos | S |
| `CEST` | Código Especificador da Substituição Tributária. Obrigatório para produtos sujeitos a ST. | 7 dígitos | C |
| `cBenef` | Código de benefício fiscal, quando a UF exige. | Texto 8–10 | C |
| `EXTIPI` | Exceção da tabela do IPI. | 2–3 dígitos | N |
| `CFOP` | Código Fiscal de Operações. 5xxx = mesma UF · 6xxx = outra UF · 7xxx = exterior. | 4 dígitos | S |
| `uCom` | Unidade comercial (UN, CX, KG...). | Texto 1–6 | S |
| `qCom` | Quantidade comercial. | Até 4 casas decimais | S |
| `vUnCom` | Valor unitário comercial. | Até 10 casas decimais | S |
| `vProd` | Valor total bruto do item (`qCom` × `vUnCom`). | 2 casas decimais | S |
| `cEANTrib` | Código de barras da unidade tributável. Mesmas regras do `cEAN`. | GTIN ou `SEM GTIN` | S |
| `uTrib` / `qTrib` / `vUnTrib` | Unidade, quantidade e valor unitário tributáveis. Normalmente iguais aos comerciais. | — | S |
| `vFrete` / `vSeg` / `vOutro` | Frete, seguro e outras despesas rateados no item. | 2 casas decimais | N |
| `vDesc` | Desconto do item. | 2 casas decimais | N |
| `indTot` | 1 = o `vProd` entra no total da nota · 0 = não entra. | 0 ou 1 | S |
| `xPed` / `nItemPed` | Número do pedido de compra do cliente e item do pedido. | — | N |
| `infAdProd` | Informação adicional do item (fica no `det`, depois do `imposto`). | Texto 1–500 | N |


## det / imposto — Impostos do item

### Geral

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `vTotTrib` | Valor aproximado dos tributos (Lei da Transparência 12.741/12). | 2 casas decimais | N |

### ICMS

O grupo usado depende do regime (`CRT`) e da situação tributária. Exemplos: `ICMS00`, `ICMS10`, `ICMS60` (regime normal) e `ICMSSN102`, `ICMSSN500` (Simples Nacional).

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `orig` | Origem da mercadoria: 0 = nacional · 1 = estrangeira (importação direta) · 2 = estrangeira (mercado interno) · 3 a 8 = outras situações de conteúdo de importação. | 0 a 8 | S |
| `CST` | Situação tributária do ICMS (regime normal), ex.: 00, 10, 20, 40, 60. | 2 dígitos | C |
| `CSOSN` | Situação tributária do Simples Nacional, ex.: 101, 102, 500, 900. | 3 dígitos | C |
| `modBC` | Como a base de cálculo é determinada (0 = MVA, 3 = valor da operação...). | 1 dígito | C |
| `vBC` / `pICMS` / `vICMS` | Base de cálculo, alíquota e valor do ICMS. | — | C |
| `modBCST` / `pMVAST` | Forma de cálculo da base da ST e percentual de MVA. | — | C |
| `vBCST` / `pICMSST` / `vICMSST` | Base, alíquota e valor do ICMS-ST. | — | C |
| `vBCSTRet` / `pST` / `vICMSSTRet` | ST retida anteriormente (CST 60 / CSOSN 500). | — | C |
| `pCredSN` / `vCredICMSSN` | Percentual e valor do crédito de ICMS permitido no Simples (CSOSN 101/201). | — | C |
| `vICMSDeson` / `motDesICMS` | ICMS desonerado e o motivo. | — | C |
| `pFCP` / `vFCP` | Fundo de Combate à Pobreza. | — | C |

### IPI

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `cEnq` | Código de enquadramento legal do IPI (999 = tributação normal). | 3 dígitos | C |
| `CST` | Situação tributária do IPI (ex.: 50, 53, 99). | 2 dígitos | C |
| `vBC` / `pIPI` / `vIPI` | Base, alíquota e valor do IPI. | — | C |

### PIS e COFINS

Mesma estrutura nos dois. Grupos: `PISAliq`, `PISNT`, `PISOutr`... e `COFINSAliq`, `COFINSNT`, `COFINSOutr`...

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CST` | Situação tributária (01 = tributável · 04 = monofásico · 06 = alíquota zero · 07 = isento · 49 = outras saídas · 99 = outras). | 2 dígitos | S |
| `vBC` / `pPIS` / `vPIS` | Base, alíquota e valor do PIS. | — | C |
| `vBC` / `pCOFINS` / `vCOFINS` | Base, alíquota e valor da COFINS. | — | C |

### IBS e CBS (Reforma Tributária)

Grupo novo, criado pela NT 2025.002 (ver pasta `reforma_tributaria`). Confirme sempre a versão vigente da NT.

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `IBSCBS` | Grupo dos novos tributos do item. | — | C |
| `CST` | Situação tributária do IBS/CBS. | 3 dígitos | C |
| `cClassTrib` | Código de classificação tributária. | 6 dígitos | C |
| `vBC` | Base de cálculo do IBS/CBS. | 2 casas decimais | C |
| `gIBSUF` → `pIBSUF` / `vIBSUF` | Alíquota e valor do IBS estadual. | — | C |
| `gIBSMun` → `pIBSMun` / `vIBSMun` | Alíquota e valor do IBS municipal. | — | C |
| `gCBS` → `pCBS` / `vCBS` | Alíquota e valor da CBS (federal). | — | C |


## total / ICMSTot — Totais da nota

Os totais precisam bater com a soma dos itens. Se não baterem, a SEFAZ rejeita a nota (ex.: rejeição 564 para o total de produtos e 610 para o total da nota).

| Tag | O que é |
|---|---|
| `vBC` / `vICMS` | Soma da base e do valor do ICMS dos itens. |
| `vICMSDeson` | Soma do ICMS desonerado. |
| `vFCP` / `vFCPST` | Soma do FCP e do FCP-ST. |
| `vBCST` / `vST` | Soma da base e do valor do ICMS-ST. |
| `vProd` | Soma do `vProd` dos itens com `indTot` = 1. |
| `vFrete` / `vSeg` / `vDesc` / `vOutro` | Soma de frete, seguro, desconto e outras despesas. |
| `vII` / `vIPI` / `vIPIDevol` | Imposto de importação, IPI e IPI devolvido. |
| `vPIS` / `vCOFINS` | Soma do PIS e da COFINS. |
| `vNF` | **Valor total da nota** = vProd − vDesc − vICMSDeson + vST + vFCPST + vFrete + vSeg + vOutro + vII + vIPI + vIPIDevol. |
| `vTotTrib` | Soma do valor aproximado dos tributos. |


## transp — Transporte

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `modFrete` | Responsável pelo frete: 0 = emitente (CIF) · 1 = destinatário (FOB) · 2 = terceiros · 3 = transporte próprio do remetente · 4 = transporte próprio do destinatário · 9 = sem frete. | 1 dígito | S |
| `transporta` | Dados da transportadora (CNPJ/CPF, xNome, IE, xEnder, xMun, UF). | — | N |
| `veicTransp` | Placa e UF do veículo. | — | N |
| `vol` → `qVol` / `esp` / `marca` / `pesoL` / `pesoB` | Volumes: quantidade, espécie, marca, peso líquido e peso bruto. | — | N |


## cobr — Cobrança

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `fat` → `nFat` / `vOrig` / `vDesc` / `vLiq` | Fatura: número, valor original, desconto e valor líquido. | — | N |
| `dup` → `nDup` | Número da parcela, em sequência: `001`, `002`... | Texto 1–60 | C |
| `dup` → `dVenc` | Vencimento da parcela. | AAAA-MM-DD | C |
| `dup` → `vDup` | Valor da parcela. | 2 casas decimais | C |


## pag — Pagamento

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `detPag` | Uma forma de pagamento (pode repetir). | — | S |
| `indPag` | 0 = à vista · 1 = a prazo. | 0 ou 1 | N |
| `tPag` | Meio de pagamento: 01 = dinheiro · 02 = cheque · 03 = cartão de crédito · 04 = cartão de débito · 05 = crédito loja · 15 = boleto · 16 = depósito · 17 = PIX dinâmico · 18 = transferência / carteira digital · 20 = PIX estático · **90 = sem pagamento** (devolução, ajuste, remessa) · 99 = outros. | 2 dígitos | S |
| `xPag` | Descrição do meio de pagamento. Obrigatório quando `tPag` = 99. | Texto 2–60 | C |
| `vPag` | Valor pago nesse meio. | 2 casas decimais | S |
| `card` → `tpIntegra` | 1 = pagamento integrado ao sistema (TEF) · 2 = não integrado (POS). | 1 ou 2 | C |
| `card` → `CNPJ` / `tBand` / `cAut` | CNPJ da credenciadora, bandeira e código de autorização. | — | N |
| `vTroco` | Valor do troco. | 2 casas decimais | N |


## infAdic — Informações adicionais

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `infAdFisco` | Informações de interesse do fisco. | Texto 1–2000 | N |
| `infCpl` | Informações complementares de interesse do contribuinte (aparecem no DANFE). | Texto 1–5000 | N |


## infRespTec — Responsável técnico

Dados da empresa que desenvolveu o sistema emissor.

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CNPJ` | CNPJ da software house. | 14 dígitos | C |
| `xContato` / `email` / `fone` | Contato técnico. | — | C |


## Retorno da SEFAZ

| Tag | O que é |
|---|---|
| `retEnviNFe` | Resposta ao envio do lote. |
| `cStat` | **Código do resultado.** 100 = autorizada · 103 = lote recebido · 104 = lote processado · demais = rejeição (ver pasta `3 - Retornos`). |
| `xMotivo` | Descrição do resultado (a mensagem da rejeição). |
| `nRec` | Número do recibo, usado para consultar o lote no modo assíncrono. |
| `protNFe` / `infProt` | Protocolo de cada nota. |
| `chNFe` | Chave de acesso da nota. |
| `nProt` | Número do protocolo de autorização. |
| `dhRecbto` | Data e hora do recebimento na SEFAZ. |
| `digVal` | Resumo (hash) da nota assinada. |
