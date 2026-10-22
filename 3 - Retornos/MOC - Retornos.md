# MOC — Retornos

> 🚧 **Em construção.** Este mapa é alimentado aos poucos, à medida que novas rejeições são encontradas e documentadas.

## Para que serve esta pasta

Aqui ficam registradas as **rejeições e erros retornados** pela SEFAZ (ou pela prefeitura, no caso de serviço) durante a emissão de documentos fiscais pelo sistema. Cada nota explica:

• qual foi a mensagem de retorno;
• o que causou o erro;
• um exemplo do XML rejeitado, quando houver;
• como corrigir.

O objetivo é servir de consulta rápida para o suporte e para o desenvolvimento quando uma emissão for recusada.


## Como está organizada

| Pasta | Documento | Uso |
|---|---|---|
| `NF-e (modelo 55)` | Nota Fiscal Eletrônica | Venda de peças / mercadorias |
| `NFC-e (modelo 65)` | Nota Fiscal de Consumidor Eletrônica | Cupom fiscal |
| `NFS-e (serviço)` | Nota Fiscal de Serviço Eletrônica | Prestação de serviço |

**Padrão de nome dos arquivos:** `<código> - <descrição curta>.md`
Exemplo: `225 - Falha no Schema XML - cEAN inválido.md`

**Para cadastrar uma nova rejeição:** copie o [[_Modelo de retorno]], preencha, salve na pasta do documento correspondente e adicione o link na seção certa abaixo.


## NF-e (modelo 55) — Peças

_Nenhuma rejeição documentada ainda._


## NFC-e (modelo 65) — Cupom

| Código | Rejeição | Assunto |
|---|---|---|
| 225 | [[225 - Falha no Schema XML - cEAN inválido]] | Produto / código de barras |


## NFS-e — Serviço

_Nenhuma rejeição documentada ainda._


## Relacionados

• [[carta-de-correção]] — o que pode ser corrigido após a autorização da NF-e
• [[Emissão de NF-e em operação interestadual]] — regra de CFOP que evita rejeição em vendas para outro estado
