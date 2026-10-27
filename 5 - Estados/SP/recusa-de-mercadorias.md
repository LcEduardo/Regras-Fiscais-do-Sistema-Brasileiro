# Recusa de Mercadorias — Emissão de NF-e

*Elaborado em 27/10/2026, com base em orientação da Sefaz-SP. Confirme a orientação do estado de cada parte antes de emitir.*

A partir de **01/01/2027**, na **recusa parcial** de mercadorias por destinatário **contribuinte do ICMS**, quem emite a nota passa a ser o **destinatário** (nota de débito), e não mais o remetente. Nos demais casos, nada muda.

> "Contribuinte" aqui significa **contribuinte do ICMS**, e não do IBS. Prestadores de serviço seguem a documentação de IBS/CBS, que é outra.


## Fundamento legal

• Art. 453 do RICMS/SP — NF-e de entrada na recusa (com as adaptações do Ajuste SINIEF 49/2025).
• Ajuste SINIEF 49/2025 — produz efeitos desde 03/08/2026 (uso facultativo).
• Ajuste SINIEF 8/2026 — revogou a regra que diferenciava a emissão pela condição do destinatário.
• Ajuste SINIEF 34/2026 — restabeleceu a distinção entre contribuinte e não contribuinte.
• Respostas à Consulta Sefaz-SP 21.837/2020, 33.490/2026 e 33.157/2026.


## Quem emite o quê

| Situação | Quem emite | Documento |
|---|---|---|
| Recusa total | Remetente | NF-e de entrada |
| Recusa parcial, destinatário **não** contribuinte do ICMS (inclui quem tem IE mas não é contribuinte) | Remetente | NF-e de entrada |
| Recusa parcial, destinatário contribuinte do ICMS, **a partir de 01/01/2027** | **Destinatário** | NF-e de saída, na forma de **nota de débito**, referenciando a nota original e destacando o ICMS quando devido |

Exemplo: você vende 10 caixas para o Cliente A, e ele recusa na entrega.
• Recusa as 10 → você emite a NF-e de entrada.
• Recusa 3 e é contribuinte do ICMS → a partir de 2027, **ele** emite a nota de débito das 3 caixas, referenciando a sua nota.
• Recusa 3 e não é contribuinte do ICMS (ex.: pessoa física) → você emite a NF-e de entrada das 3 caixas.


## Devolução recusada pelo fornecedor

Caso: a NF-e de devolução foi emitida, o fornecedor recusou e o prazo de cancelamento já passou. O fornecedor é o destinatário da nota de devolução, então a regra de recusa se aplica a ele **por analogia** (a orientação trata de recusa de vendas — confirmar).

• Recusa total → o emitente da devolução emite a NF-e de entrada.
• Recusa parcial, fornecedor contribuinte do ICMS → a partir de 01/01/2027, o fornecedor emite a nota de débito. Até lá, vale o procedimento anterior (Resposta à Consulta 21.837/2020); a nova regra é facultativa desde 03/08/2026.
• Recusa parcial, fornecedor não contribuinte do ICMS → o emitente da devolução emite a NF-e de entrada.


## Histórico da regra

| Data | O que aconteceu |
|---|---|
| 2020 | Resposta à Consulta 21.837/2020: a recusa parcial seguia o procedimento da recusa total, com adaptações |
| 2026 (data não informada) | Ajuste SINIEF 8/2026 revogou a regra que diferenciava a emissão pela condição do destinatário |
| 12/05/2026 | Resposta à Consulta 33.490/2026: remetente emitia NF-e de entrada (nota de crédito) em toda recusa parcial |
| 03/08/2026 | Ajuste SINIEF 49/2025 passa a produzir efeitos; uso facultativo |
| 06/10/2026 | Resposta à Consulta 33.157/2026 publicada, após o Ajuste SINIEF 34/2026 restabelecer a distinção |
| **01/01/2027** | **Obrigatório para contribuintes paulistas** |


## Pontos a confirmar antes de emitir

• A recusa foi total ou parcial?
• O destinatário (fornecedor ou cliente) é contribuinte do ICMS?
• Em qual estado cada parte está? O Ajuste SINIEF é nacional, mas cada Sefaz pode orientar de forma própria.
• Quais códigos de `finNFe`, `tpNFDebito` / `tpNFCredito` e CFOP valem para a nota de débito de recusa parcial? Confirmar no Ajuste SINIEF 49/2025 e na NT vigente.
• Como tratar a devolução recusada após o prazo de cancelamento? Confirmar com o contador ou com a Sefaz.


## Fontes

• [Portal Contábeis: Recusa parcial de mercadorias muda emissão de nota fiscal em SP em 2027](https://www.contabeis.com.br/noticias/80403/recusa-parcial-de-mercadorias-muda-emissao-de-nota-fiscal-em-sp-em-2027/)
• [Resposta à Consulta Tributária 33.157/2026, Sefaz-SP](https://legislacao.fazenda.sp.gov.br/Paginas/RC33157_2026.aspx) — citada pela notícia, não aberta diretamente.


## Ver também

• Regras de devolução: `2 - Regras/devolução.md`.
