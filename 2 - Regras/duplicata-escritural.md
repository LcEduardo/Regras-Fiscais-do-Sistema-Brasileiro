# Duplicata Escritural

*Elaborado em 27/10/2026, com base em notícia do Portal Contábeis e em comunicado do Ministério da Fazenda de 26/10/2026. Confirme a regulamentação vigente do Banco Central antes de orientar um cliente.*

A duplicata deixa de ser papel ou um boleto avulso e passa a ser **registrada em um sistema eletrônico autorizado pelo Banco Central** (a escrituradora). A partir de **julho de 2027**, para **grandes empresas**, e depois para os demais portes, o registro é obrigatório quando a duplicata for usada em uma **operação de crédito**.

> **Não muda nada no layout da NF-e.** O grupo `cobr` continua opcional e a SEFAZ não consulta a escrituradora. Uma NF-e sem `dup`, ou com `dup` diferente da duplicata registrada, continua sendo autorizada.


## Fundamento legal

• Lei nº 13.775/2018 — cria a duplicata escritural (emissão sob a forma eletrônica).
• Lei nº 5.474/1968 (Lei das Duplicatas), art. 8º — motivos que permitem ao comprador recusar o aceite.
• Código Penal, art. 172 — duplicata simulada (emitir duplicata sem venda ou serviço real).
• Regulamentação do CMN e do Banco Central — regras operacionais das escrituradoras e da obrigatoriedade. A numeração das resoluções vigentes ainda precisa ser confirmada.
• Comunicado do Ministério da Fazenda de 26/10/2026 — cronograma por porte.


## Conceitos

### Duplicata

É o **direito de receber** uma venda a prazo.

Exemplo: sua empresa vende R$ 10.000 para um cliente, com pagamento em 60 dias. Você emite a NF-e e passa a ter uma duplicata: o direito de receber R$ 10.000 daqui a 60 dias.

### Operação de crédito

É quando a empresa **usa a duplicata para conseguir dinheiro antes do prazo**.

| Tipo | Como funciona (venda de R$ 10.000 em 60 dias) |
|---|---|
| Desconto / antecipação | Você leva a duplicata ao banco, ele te paga cerca de R$ 9.700 hoje e recebe os R$ 10.000 do cliente em 60 dias. A diferença é o lucro do banco. |
| Garantia de empréstimo | Você pega um empréstimo e oferece as duplicatas como garantia. Se não pagar, o banco fica com elas. |
| Venda para fundo ou factoring | Igual ao desconto, mas com uma empresa que compra recebíveis em vez de um banco. |

**Se a empresa só espera os 60 dias e recebe do cliente, não há operação de crédito.** Nesse caso, a obrigação nova praticamente não a atinge.

### Escrituradora

É um **"cartório digital" de duplicatas**: uma empresa autorizada pelo Banco Central que mantém o registro oficial de cada duplicata.

O problema que ela resolve: hoje é possível levar a **mesma** duplicata de R$ 10.000 a três bancos diferentes e antecipar nos três, porque um banco não sabe o que o outro fez. Isso é fraude, mas acontece.

Com a escrituradora:
1. A duplicata é registrada (quem emitiu, quem deve, valor, vencimento).
2. Quando é antecipada com o Banco A, isso fica registrado.
3. Se alguém tentar levá-la ao Banco B, ele consulta e vê que a duplicata **já está com o Banco A**.

Ela também registra o que acontece depois: aceite ou recusa do cliente, pagamento, devolução.

> Comparação: a **SEFAZ** autoriza e guarda a **nota fiscal**. A **escrituradora** faz o mesmo papel para a **duplicata**. São sistemas separados, e por isso a SEFAZ não confere se a nota bate com a duplicata.

Os financiadores (bancos, fundos) só consultam os dados da duplicata com **autorização expressa do fornecedor**.


## Quem é afetado

| Situação | O que muda |
|---|---|
| Vende a prazo e só espera receber | Nada por enquanto. |
| Antecipa ou dá duplicatas em garantia | A partir de julho de 2027 (grandes empresas primeiro), a duplicata precisa estar registrada em uma escrituradora. |
| Compra a prazo (é o devedor) | Precisa acompanhar os avisos da escrituradora e aceitar ou recusar a duplicata eletronicamente, no prazo e com motivo legal. |

> **Atenção, comprador:** se o contas a pagar não acompanhar os avisos, a empresa pode ficar com um título aceito e já cedido a um banco que ela nem conhece.


## Relação com a NF-e

A nota não é validada contra a duplicata, mas **a duplicata precisa corresponder a uma venda real**, e a NF-e é a prova disso. Quando os dados não batem, o problema aparece fora da SEFAZ:

| Divergência | Consequência |
|---|---|
| Valor ou vencimento da duplicata diferente do `dup` da NF-e | O financiador pode recusar a antecipação ou travar a conciliação. |
| Duplicata sem nota válida por trás (ou com nota cancelada) | Duplicata simulada, que é **crime** (art. 172 do CP). Agora fica rastreável. |
| Devolução ou recusa não refletida no título | O comprador pode recusar a duplicata, e o banco que a antecipou cobra de volta do fornecedor. |

**Recomendação para o sistema:** preencher o grupo `cobr` da NF-e com as **mesmas parcelas** que serão registradas na escrituradora, gerando as duas a partir da mesma fonte no ERP.

| Tag | Deve bater com |
|---|---|
| `fat` → `nFat` / `vLiq` | Número e valor total dos títulos |
| `dup` → `nDup` | Número da parcela registrada |
| `dup` → `dVenc` | Vencimento da duplicata |
| `dup` → `vDup` | Valor da duplicata |

Detalhes das tags: `4 - Layout XML/NF-e (modelo 55).md`, seção **cobr — Cobrança**.


## Casos especiais

| Situação fiscal | Efeito na duplicata escritural |
|---|---|
| Recusa de mercadoria | É motivo legal de recusa do título (art. 8º da Lei 5.474/68). A recusa fiscal e a da duplicata precisam andar juntas. |
| Devolução (parcial ou total) | Gera abatimento ou cancelamento que precisa ser registrado na duplicata. Se o título já foi antecipado, o banco precisa saber. |
| CC-e | Não pode alterar valor nem quantidade. Um erro desse tipo na fatura exige outro caminho também do lado da duplicata. |
| Remessas sem cobrança (CFOP 5.949, `tPag` = 90) | Não geram duplicata. |


## Preparação da empresa

• Mapear quem emite, confere, antecipa e liquida as duplicatas.
• Escolher a escrituradora (diretamente ou pelo banco) e ver como o ERP vai trocar dados com ela.
• Verificar se a empresa e suas operações entram no cronograma.
• Testar os fluxos antes do prazo.
• Definir responsáveis por aceite, recusa, conciliação e autorização de acesso aos dados.


## Pontos a confirmar

• Qual resolução do CMN / Banco Central está vigente para a duplicata escritural?
• Qual o critério de **grande empresa** usado no cronograma (faturamento, Lei 11.638/2007 ou outro)?
• Qual o prazo para os demais portes?
• O registro na escrituradora precisa informar a **chave da NF-e** como lastro?


## Fontes

• [Portal Contábeis: Duplicata escritural muda gestão de recebíveis e exige atenção das empresas](https://www.contabeis.com.br/noticias/80393/duplicata-escritural-o-que-muda-para-as-empresas-e-o-credito/)
• Comunicado do Ministério da Fazenda de 26/10/2026 — citado pela notícia, não aberto diretamente.


## Ver também

• Recusa de mercadorias: `5 - Estados/SP/recusa-de-mercadorias.md`.
• Devolução: `2 - Regras/devolução.md`.
• Carta de Correção: `2 - Regras/carta-de-correção.md`.
• Remessas e CFOP 5.949: `2 - Regras/remessa.md`.
