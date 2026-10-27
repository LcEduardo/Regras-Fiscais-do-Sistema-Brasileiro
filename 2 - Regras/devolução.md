# Devolução de Mercadoria — Cálculo do ICMS

A NF-e de devolução desfaz, total ou parcialmente, uma operação anterior. Por isso ela deve destacar o ICMS (e, quando houver, ICMS-ST, FCP e IPI) **nas mesmas condições da nota original**, para anular o crédito e o débito gerados na compra.


## Fundamento legal

• Ajuste SINIEF 07/05 — NF-e e regras do documento referenciado.
• MOC da NF-e — `finNFe = 4` (Devolução) e obrigatoriedade do grupo `NFref`.
• NT 2016.002 — criação do campo `vIPIDevol` (IPI devolvido).
• Resolução CGSN 140/2018 — devolução emitida por optante do Simples Nacional.
• RICMS de cada UF — direito ao crédito do ICMS pelo estabelecimento que recebe a devolução.


## Como fica o crédito e o débito

| Etapa | Fornecedor (vendeu) | Comprador (devolve) |
|---|---|---|
| Venda original | **Debita** o ICMS | **Credita** o ICMS (se tiver direito) |
| Devolução | **Credita** o ICMS destacado na devolução | **Debita** o ICMS destacado na devolução |
| Resultado | Débito anulado | Crédito anulado |

• Mesmo que o comprador **não** tenha tomado crédito na entrada (ex.: uso e consumo), o ICMS deve ser destacado na devolução: é esse destaque que permite ao fornecedor estornar o débito.


## Regras do cálculo

• **Base de cálculo e alíquota da nota original** — não recalcular pela alíquota vigente na data da devolução.
• **Devolução parcial** — valores proporcionais à quantidade devolvida (base, ICMS, ICMS-ST, FCP, FCP-ST e IPI).
• **ICMS-ST** — se a nota original teve ST, devolver também `vBCST`, `vICMSST` e, se houver, `vFCPST`.
• **IPI** — informado em `vIPIDevol` (grupo `impostoDevol`), e não em `vIPI`.
• **Frete, seguro, desconto e outras despesas** — acompanham a proporção do que foi devolvido, quando compuseram a base na nota original.

Exemplo (devolução parcial):
• Nota original: 10 un × R$ 100,00 = R$ 1.000,00 · alíquota 18% · ICMS R$ 180,00.
• Devolução de 3 un: base R$ 300,00 · alíquota 18% · ICMS **R$ 54,00**.


## Campos da NF-e de devolução

| Campo | Valor |
|---|---|
| `finNFe` | `4` — Devolução de mercadoria |
| `NFref/refNFe` | Chave de acesso da nota original (obrigatório) |
| `CFOP` | Ver tabela abaixo |
| `CST` / `CSOSN` | Normalmente o mesmo tratamento tributário da nota original |
| `impostoDevol/pDevol` | Percentual devolvido da mercadoria |
| `impostoDevol/IPI/vIPIDevol` | IPI devolvido |

• Sem documento referenciado, a SEFAZ rejeita a nota (**Rejeição 321 — NF-e de devolução de mercadoria não possui documento referenciado**).


## CFOP mais comuns

| Operação original | Interna | Interestadual |
|---|---|---|
| Compra para industrialização | 5.201 | 6.201 |
| Compra para comercialização | 5.202 | 6.202 |
| Compra para industrialização com ST | 5.410 | 6.410 |
| Compra para comercialização com ST | 5.411 | 6.411 |
| Compra para uso e consumo com ST | 5.413 | 6.413 |
| Compra para ativo imobilizado | 5.553 | 6.553 |
| Compra para uso e consumo | 5.556 | 6.556 |


## Casos especiais

• **Comprador do Simples Nacional** — destaca o ICMS na devolução (CSOSN 900) com a base e a alíquota da nota original, para que o fornecedor recupere o crédito.
• **Comprador não contribuinte (consumidor final, pessoa física)** — não emite nota. O fornecedor emite **NF-e de entrada própria** (`tpNF = 0`, `finNFe = 4`), referenciando a nota de venda, e se credita do ICMS destacado nela.
• **Devolução interestadual com DIFAL** — o DIFAL recolhido na operação original pode ser recuperado conforme a legislação da UF de destino; não há destaque de DIFAL na nota de devolução.


## Ver também

• Processo interno de emissão: `processos/Emissao_fiscal_devolucao`.
• Remessas (inclusive a 6.923 que acompanha a devolução) e CFOP 5.949: `2 - Regras/remessa.md`.
