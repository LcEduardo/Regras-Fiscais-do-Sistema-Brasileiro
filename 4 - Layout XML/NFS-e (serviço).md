# Layout XML — NFS-e (serviço)

> 🚧 **Em construção.** Explica o que cada tag do XML da NFS-e faz, para quem trabalha com webservice.
>
> **Dica:** use Ctrl+F com o nome da tag que veio na rejeição.

A NFS-e **não tem um leiaute único** como a NF-e. Existem dois cenários:

| Cenário | Leiaute | Para onde envia |
|---|---|---|
| **Padrão Nacional** | DPS (Declaração de Prestação de Serviço), do Sistema Nacional NFS-e | Ambiente nacional ou prefeitura conveniada |
| **Padrão da prefeitura** | ABRASF ou leiaute próprio do provedor (cada município pode ter o seu) | Webservice da prefeitura |

Este arquivo descreve principalmente o **Padrão Nacional (DPS)**. No final há uma tabela de equivalência com as tags do ABRASF. Como os leiautes mudam por município e por versão, confira sempre a documentação oficial do município.

**Legenda — Obrig.:** S = obrigatória · N = opcional · C = condicional


## Estrutura geral (Padrão Nacional)

```
DPS
└── infDPS              → conteúdo da declaração
    ├── (identificação) → ambiente, data, série, número, competência
    ├── prest           → prestador do serviço (a empresa)
    ├── toma            → tomador do serviço (o cliente)
    ├── serv            → serviço prestado
    │   ├── locPrest    → onde o serviço foi prestado
    │   └── cServ       → códigos e descrição do serviço
    └── valores         → valores e tributação
        ├── vServPrest
        └── trib
            ├── tribMun → ISSQN
            ├── tribFed → tributos federais
            └── totTrib
```


## infDPS — Identificação

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `infDPS` | Conteúdo da DPS. Atributo `Id` formado pelos dados do emitente, série e número. | — | S |
| `tpAmb` | Ambiente: 1 = produção · 2 = homologação. | 1 ou 2 | S |
| `dhEmi` | Data e hora de emissão da DPS. | Data/hora UTC | S |
| `verAplic` | Versão do sistema emissor. | Texto | S |
| `serie` | Série da DPS. Atenção: as faixas de série podem ser reservadas por canal de emissão (ver caso de Teresina abaixo). | Texto, até 5 | S |
| `nDPS` | Número da DPS. | Numérico | S |
| `dCompet` | Data de competência (quando o serviço foi prestado). | AAAA-MM-DD | S |
| `tpEmit` | Quem emite: 1 = prestador · 2 = tomador · 3 = intermediário. | 1 dígito | S |
| `cLocEmi` | Código IBGE do município emissor. | 7 dígitos | S |
| `subst` | Dados da NFS-e substituída, quando a nota é uma substituição. | — | C |


## prest — Prestador

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CNPJ` / `CPF` | Documento do prestador. | 14 / 11 dígitos | S |
| `IM` | Inscrição municipal. | Texto | C |
| `fone` / `email` | Contato do prestador. | — | N |
| `regTrib` → `opSimpNac` | Situação no Simples Nacional: 1 = não optante · 2 = MEI · 3 = ME/EPP. | 1 dígito | S |
| `regTrib` → `regApTribSN` | Regime de apuração dos tributos no Simples (quando optante). | 1 dígito | C |
| `regTrib` → `regEspTrib` | Regime especial de tributação (0 = nenhum; demais conforme leiaute). | 1 dígito | S |


## toma — Tomador

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `CNPJ` / `CPF` / `NIF` | Documento do tomador (NIF para estrangeiro). | — | C |
| `IM` | Inscrição municipal do tomador. | Texto | N |
| `xNome` | Nome ou razão social. | Texto | C |
| `end` | Endereço (`endNac` → `cMun`, `CEP`; `xLgr`, `nro`, `xBairro`...). | — | N |
| `fone` / `email` | Contato do tomador. | — | N |


## serv — Serviço

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `locPrest` → `cLocPrestacao` | Código IBGE do município onde o serviço foi prestado. Define, em muitos casos, onde o ISS é devido. | 7 dígitos | S |
| `cServ` → `cTribNac` | **Código de tributação nacional:** item + subitem da lista da LC 116/03 + desdobro, **sem pontos**. Ex.: `14.01.01` → `140101`. | 6 dígitos | S |
| `cServ` → `cTribMun` | **Código de tributação municipal:** complemento definido pela prefeitura. | 3 dígitos | C |
| `cServ` → `xDescServ` | Descrição do serviço prestado. | Texto 1–2000 | S |
| `cServ` → `cNBS` | Código da Nomenclatura Brasileira de Serviços. | 9 dígitos | C |

**Exemplo (Teresina):** Código Complementar Municipal `14.01.01.045` → `cTribNac` = `140101` e `cTribMun` = `045`. Ver [Configuração Teresina](<../5 - Estados/PI/Teresina/Configuração.md>).


## valores — Valores e tributação

| Tag | O que é | Formato | Obrig. |
|---|---|---|---|
| `vServPrest` → `vServ` | Valor do serviço prestado. | 2 casas decimais | S |
| `vDescCondIncond` → `vDescIncond` | Desconto incondicionado (reduz a base do ISS). | 2 casas decimais | N |
| `vDescCondIncond` → `vDescCond` | Desconto condicionado (não reduz a base do ISS). | 2 casas decimais | N |
| `trib` → `tribMun` → `tribISSQN` | Tributação do ISS: 1 = operação tributável · 2 = imunidade · 3 = exportação de serviço · 4 = não incidência. | 1 dígito | S |
| `tribMun` → `tpRetISSQN` | Retenção do ISS: 1 = não retido · 2 = retido pelo tomador · 3 = retido pelo intermediário. | 1 dígito | S |
| `tribMun` → `pAliq` | Alíquota do ISS. | 2 casas decimais | C |
| `trib` → `tribFed` | Tributos federais (PIS, COFINS, IRRF, CSLL, INSS retidos). | — | N |
| `trib` → `totTrib` | Valor aproximado dos tributos (Lei 12.741/12). | — | S |


## Equivalência com o padrão ABRASF

Para prefeituras que não usam o Padrão Nacional.

| Padrão Nacional | ABRASF (aproximado) | O que é |
|---|---|---|
| `prest` | `Prestador` / `PrestadorServico` | Prestador |
| `toma` | `Tomador` / `TomadorServico` | Tomador |
| `nDPS` / `serie` | `IdentificacaoRps` → `Numero` / `Serie` | Número e série do RPS/DPS |
| `dCompet` | `Competencia` | Data de competência |
| `cTribNac` | `ItemListaServico` | Item da LC 116 (no ABRASF costuma ir com ponto, ex.: `14.01`) |
| `cTribMun` | `CodigoTributacaoMunicipio` | Código municipal |
| `xDescServ` | `Discriminacao` | Descrição do serviço |
| `vServ` | `ValorServicos` | Valor do serviço |
| `pAliq` | `Aliquota` | Alíquota do ISS |
| `tpRetISSQN` | `IssRetido` (1 = sim · 2 = não) | Retenção do ISS |
| `cLocPrestacao` | `CodigoMunicipio` / `MunicipioIncidencia` | Município da prestação / incidência |
| `opSimpNac` | `OptanteSimplesNacional` (1 = sim · 2 = não) | Simples Nacional |


## Particularidades por município

| Município | Observação |
|---|---|
| Teresina (PI) | Série via webservice entre **10001 e 49999**. A série 00001 é reservada para emissão no próprio sistema municipal. Ver [Configuração Teresina](<../5 - Estados/PI/Teresina/Configuração.md>). |
