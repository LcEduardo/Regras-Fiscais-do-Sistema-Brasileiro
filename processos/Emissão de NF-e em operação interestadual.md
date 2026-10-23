# Emissão de NF-e em operação interestadual

## Quando se aplica

Uma NF-e é **interestadual** quando o cliente (destinatário) está em um estado diferente do
estado da empresa emitente. Exemplo: empresa em SP vendendo para cliente em MG.

Nesse tipo de operação a SEFAZ exige:

- **CFOP iniciado em 6** (ex.: 6102, 6404). Os CFOPs iniciados em 5 (5102, 5405) só valem
  para operações dentro do mesmo estado.
- **Destino da operação = 2 (interestadual)** no XML da nota.

Se a nota for enviada com CFOP 5xxx para um cliente de outro estado, ela é **rejeitada pela SEFAZ**.

## Como o sistema trata

O tratamento só acontece quando **todas** as condições abaixo são atendidas:

1. A nota é **NF-e** (modelo 55). NFC-e (cupom) não entra nessa regra.
2. O **cliente está informado** na nota.
3. Empresa e cliente têm **cidade cadastrada**, e os estados são diferentes.

Com essas condições atendidas, o comportamento depende da configuração **Emite NF-e interestadual**:

| Configuração | O que acontece |
|---|---|
| **Ativada** | O sistema ajusta a nota automaticamente: troca o CFOP, marca a operação como interestadual e define a presença do comprador como "não presencial". |
| **Desativada** (padrão) | O CFOP do produto é mantido como está no cadastro. |

### Conversão automática de CFOP (configuração ativada)

| CFOP no cadastro do produto | CFOP emitido na nota |
|---|---|
| 5102 – Venda de mercadoria | 6102 |
| 5405 – Venda com ST (substituído) | 6404 |
| Qualquer outro | Mantido sem alteração |

> **Atenção:** CFOPs diferentes de 5102 e 5405 **não** são convertidos. Se a empresa usa outro
> CFOP, ele precisa ser incluído na regra pelo time de desenvolvimento ou o produto deve ser
> ajustado manualmente.

### Produto já cadastrado com CFOP 6xxx

Se o produto já estiver cadastrado com CFOP iniciado em 6, o sistema marca a operação como
interestadual **mesmo com a configuração desativada**. Essa é uma alternativa para quem vende
para fora do estado só de forma pontual.

## Passo a passo para o cliente emitir

1. Confirme que **a empresa e o cliente têm cidade/estado cadastrados** corretamente.
2. Solicite ao suporte a **ativação do parâmetro "Emite NF-e interestadual"** para a empresa.
3. Confira se os produtos vendidos usam **CFOP 5102 ou 5405** (convertidos automaticamente).
   Se usarem outro CFOP, avise o suporte.
4. Emita a NF-e normalmente. O sistema faz os ajustes de CFOP e de destino da operação.

## Problemas comuns

| Sintoma | Causa provável | Solução |
|---|---|---|
| Rejeição por CFOP incompatível com destino | Parâmetro desativado e produto com CFOP 5xxx | Ativar o parâmetro ou cadastrar o produto com CFOP 6xxx |
| CFOP não foi convertido | CFOP diferente de 5102/5405 | Solicitar inclusão do CFOP na regra |
| Nota saiu como operação interna | Cliente sem cidade cadastrada ou nota emitida como NFC-e | Completar o cadastro do cliente e emitir como NF-e |

## Informações técnicas (suporte)

- Parâmetro: `EMITE_NFE_INTERESTADUAL` na tabela `empresa_parametros` (`'1'` ativa, `'0'` desativa).
- Regra implementada em `src/Model/Table/EmissaoNfeTable.php`, no método `emitirNfe`.
- Mapa de conversão de CFOP: método `cfopSaidaInterestadual()`.
- Consulta para verificar a configuração de uma empresa:

    ```sql
    SELECT empresa_id, parametro, valor
    FROM empresa_parametros
    WHERE empresa_id = :empresa_id AND parametro = 'EMITE_NFE_INTERESTADUAL';
    ```