# Regras Fiscais do Sistema Brasileiro

Base de conhecimento sobre emissão de documentos fiscais eletrônicos (NF-e, NFC-e e NFS-e), voltada ao dia a dia de um ERP para oficinas mecânicas e autopeças.

A ideia é reunir, em linguagem simples, o que o suporte e o desenvolvimento precisam consultar com frequência:

• **as regras** — o que a legislação exige e como calcular os impostos;
• **os erros** — por que a SEFAZ ou a prefeitura rejeitou uma nota e como corrigir;
• **o XML** — o que cada tag significa;
• **o contexto interno** — processos do time e particularidades de clientes e municípios.

> ⚠️ **Não é consultoria tributária.** O conteúdo é de uso interno e pode ficar desatualizado. Antes de alterar uma regra fiscal no sistema, confirme com a contabilidade e com o texto oficial (legislação, MOC e Notas Técnicas vigentes). Vários pontos variam conforme o RICMS de cada UF.


## Estrutura do repositório

| Pasta | O que tem |
|---|---|
| `1 - Regras/` | Regras fiscais por assunto: quando se aplicam, como calcular, quais campos preencher. |
| `2 - Retornos/` | Rejeições e erros de emissão, separados por documento (NF-e, NFC-e e NFS-e), com causa, exemplo de XML e correção. |
| `3 - Layout XML/` | Explicação das tags do XML de cada documento, para quem trabalha com webservice. |
| `4 - Estados/` | Regras que valem só para um estado (ou município), com uma pasta por UF (`SP/`, `PI/`...). |
| `5 - Reforma Tributária/` | Reforma do consumo (EC 132/2023 e LC 214/2025): IBS, CBS e Imposto Seletivo, transição, NTs e impactos no sistema. |
| `processos/` | Como o time executa (ou o sistema trata) determinadas emissões. |
| `clientes/` | Particularidades de clientes e municípios (configurações, séries, códigos). |


## Conteúdo atual

### 1 - Regras
• `carta-de-correção.md` — o que pode e o que não pode ser corrigido com a CC-e.
• `cest.md` — quando informar o CEST, formato do código e correlação com o NCM.
• `duplicata-escritural.md` — o que é a escrituradora, quando o registro é obrigatório (jul/2027) e a relação com o grupo `cobr` da NF-e.
• `devolução.md` — cálculo do ICMS na devolução (crédito e débito), campos da NF-e e CFOP.
• `iss-retido.md` — ISS retido pelo tomador: valor líquido, campo `tpRetISSQN` da NFS-e Nacional (NT 009 / E0655) e alíquota no Simples Nacional.
• `remessa.md` — remessas (venda à ordem 5.923/6.923, conserto, comodato etc.) e o CFOP 5.949.

### 2 - Retornos
• `MOC - Retornos.md` — índice das rejeições documentadas. **Comece por aqui.**
• `_Modelo de retorno.md` — modelo para documentar uma nova rejeição.
• `NFC-e (modelo 65)/225 - Falha no Schema XML - cEAN inválido.md`
• `NFS-e (serviço)/E0120 - IM do prestador não deve ser informada.md` — quando a Inscrição Municipal vai (ou não) na DPS do Padrão Nacional.

### 3 - Layout XML
• `NF-e (modelo 55).md`
• `NFC-e (modelo 65).md`
• `NFS-e (serviço).md` — Padrão Nacional (DPS) e equivalência com o ABRASF.

### 4 - Estados
**SP**
• `recusa-de-mercadorias.md` — quem emite a nota na recusa total ou parcial (nova regra de SP a partir de 01/01/2027).
• `regra_icms_st_sp_autopecas.md` — saída das autopeças e pneus da ST em SP (Portaria SRE 34/2026), com a planilha de itens.

**PI**
• `Teresina/Configuração.md` — NFS-e de Teresina: série para webservice e código complementar municipal.

### 5 - Reforma Tributária
• Vazia por enquanto. Destinada ao IBS, à CBS, ao Imposto Seletivo e às NTs da reforma (ex.: NT 2025.002, grupo de IBS/CBS na NF-e).

### processos
• `Emissão de NF-e em operação interestadual.md` — CFOP 6xxx e destino da operação.
• `Emissao_fiscal_devolucao` — dados que precisam ser solicitados ao cliente para emitir devolução e remessa.

### clientes
• `SP/emissao_sp.md` — clientes de São Paulo que emitem nota.


## Como contribuir

• **Nova rejeição:** copie `2 - Retornos/_Modelo de retorno.md` para a pasta do documento, com o nome `<código> - <descrição curta>.md`, e adicione o link em `MOC - Retornos.md`.
• **Nova regra:** crie um arquivo em `1 - Regras/` (ou em `4 - Estados/<UF>/`, se valer só para um estado) seguindo o padrão dos existentes: descrição, **fundamento legal**, regras, campos do XML e casos especiais.
• Cite sempre a **base legal** (convênio, ajuste, NT, RICMS) e marque o que depende da UF.
• Os arquivos usam Markdown e links no estilo Obsidian (`[[nome do arquivo]]`), então a pasta pode ser aberta como um vault do Obsidian.
