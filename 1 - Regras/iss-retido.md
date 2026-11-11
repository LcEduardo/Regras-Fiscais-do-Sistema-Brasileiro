# ISS Retido: conceito, emissão da NFS-e e regras do Simples Nacional

> Material de apoio interno. Não substitui a orientação da contabilidade nem a legislação de cada município.

---

## 1. Conceito

**ISS (ISSQN)** é o imposto municipal sobre a prestação de serviços. O **prestador é o contribuinte**: o imposto é dele.

**ISS retido** é quando a lei transfere ao **tomador** a **responsabilidade de recolher** o imposto. O tomador:

1. desconta o valor do ISS do pagamento ao prestador;
2. recolhe esse valor à prefeitura, em nome do prestador.

### Retenção não é desconto

| Ideia comum (incorreta) | Como funciona de fato |
|---|---|
| "Como não pago o imposto, dou desconto ao tomador." | O imposto continua sendo do prestador. O tomador apenas repassa a parte que pertencia a ele. |
| "O valor do serviço passa a ser R$ 9.500." | O valor do serviço continua sendo R$ 10.000. R$ 9.500 é o **valor líquido** recebido. |
| "O tomador economiza R$ 500." | O tomador desembolsa os mesmos R$ 10.000: R$ 9.500 ao prestador e R$ 500 à prefeitura. |

Se fosse um desconto, a base de cálculo mudaria e o ISS seria calculado sobre R$ 9.500.

### Para qual município vai o ISS?

Nem sempre para a prefeitura do tomador. O ISS vai para o **município onde o imposto é devido**:

- **Regra geral (LC 116/2003, art. 3º):** município do estabelecimento do prestador.
- **Exceções do art. 3º:** em alguns serviços o imposto é devido no local da prestação (ex.: construção civil, limpeza, vigilância, armazenamento etc.).
- A obrigação de reter é definida pela LC 116/2003 (art. 6º) e pela **lei de cada município**.

---

## 2. Exemplo

Serviço de R$ 10.000,00, alíquota de 5%, ISS retido pelo tomador.

| Campo da NFS-e | Valor |
|---|---|
| Valor do serviço | R$ 10.000,00 |
| Base de cálculo | R$ 10.000,00 |
| Alíquota ISS | 5% |
| Valor do ISS | R$ 500,00 |
| ISS retido? | **Sim, pelo tomador** |
| **Valor líquido** | **R$ 9.500,00** |

Fluxo financeiro:

```
Tomador ──R$ 9.500──► Prestador
Tomador ──R$   500──► Prefeitura (em nome do prestador)
```

---

## 3. Dúvidas frequentes

### A nota é emitida com o valor cheio?

**Sim.** A NFS-e é emitida com R$ 10.000 de valor do serviço, ISS marcado como retido e valor líquido de R$ 9.500.

### Por que a prefeitura considera R$ 10.000 se o prestador recebeu R$ 9.500?

Porque o **faturamento bruto é R$ 10.000**, e isso está correto. O que muda é a apuração:

- a nota aparece como **ISS retido pelo tomador**;
- o prestador **não gera guia de ISS** para essa nota;
- não há bitributação.

Na contabilidade, a receita bruta é de R$ 10.000 e os R$ 500 retidos ficam separados do valor recebido.

---

## 4. Emissor Nacional (NFS-e padrão nacional)

### Campo principal: `tpRetISSQN`

Caminho no XML: `NFSe/infNFSe/DPS/infDPS/valores/trib/tribMun/tpRetISSQN`. Campo obrigatório.

| Valor | Significado |
|---|---|
| `1` | Não retido |
| `2` | Retido pelo tomador |
| `3` | Retido pelo intermediário |

### Regras de validação relevantes

- **`tpRetISSQN = 2`**: o grupo de endereço nacional do tomador precisa ser informado na DPS, exceto quando o próprio tomador emite (`tpEmit = 2`).
- **`tpRetISSQN = 3`**: mesma exigência para o intermediário, exceto quando ele é o emitente (`tpEmit = 3`).
- **Valor líquido** = valor do serviço − desconto incondicionado − retenções federais − ISS retido.
- **E0655 (NT 009):** rejeita a DPS que marca retenção (2 ou 3) quando não existe regra de retenção para o caso no município de incidência.
  - Situação em 04/11/2026: validada **apenas na produção restrita** (desde 20/10/2026). Passa a valer em produção quando a NT 009 for promovida.
- **E0596:** retenção proibida para o subitem 22.01.01 (exploração de rodovia).
- **E1506:** o total de tributos retidos não pode ser negativo.

### Pontos de atenção para o ERP / integração com a Migrate

- [ ] Confirmar com a Migrate como as regras de retenção da NT 009 serão tratadas (validação prévia, mensagens de erro, cadastro por município).
- [ ] Garantir que o endereço do tomador seja sempre enviado quando `tpRetISSQN = 2`.
- [ ] Conferir o cálculo do valor líquido com todas as retenções (ISS + federais).
- [ ] Revisar notas que hoje passam com retenção e podem começar a ser rejeitadas.

---

## 5. Simples Nacional

### Alíquota

- A alíquota retida **não é a do município**. É a **alíquota efetiva de ISS** da faixa do prestador no Simples, calculada pelo RBT12 (LC 123/2006, art. 21, § 4º).
- Pode ficar **abaixo de 2%** nas faixas iniciais.
- **Se o prestador não informar a alíquota na nota**, o tomador aplica a **maior alíquota de ISS** prevista nos Anexos III, IV ou V da LC 123/2006.
- **No mês de início de atividade**, aplica-se a **menor alíquota** prevista nesses anexos.

### No Emissor Nacional

- **E0625:** para ME/EPP (`opSimpNac = 3`), não é permitido informar alíquota quando **não há retenção** (`tpRetISSQN = 1`). A alíquota só vai na nota quando houver retenção.

### Na apuração (PGDAS-D)

- A receita é informada como **"com ISS retido"**.
- Assim, a parcela de ISS é **descontada do DAS**. Sem isso, o prestador paga o ISS duas vezes: na retenção e no DAS.

### Observação na nota

Alguns municípios exigem um texto no campo de observações, por exemplo:

> "ISS retido com alíquota de …%, conforme art. 21, § 4º, inciso I da LC 123/2006"

### Pontos de atenção para o ERP

- [ ] Preencher automaticamente a alíquota efetiva do Simples quando houver retenção.
- [ ] Não enviar alíquota quando o optante do Simples não tiver retenção (evita E0625).
- [ ] Permitir texto de observação configurável por município.

---

## 6. Resumo

1. O ISS é sempre do prestador. Na retenção, o tomador só recolhe por ele.
2. A nota sai com o **valor cheio**, ISS marcado como retido e **valor líquido** menor.
3. O faturamento do prestador é o valor bruto. O ISS retido não gera guia para ele.
4. O município de destino segue a LC 116/2003 (regra geral e exceções do art. 3º) e a lei local.
5. No padrão nacional, o campo-chave é o `tpRetISSQN`, e as novas validações (NT 009) vão restringir retenções sem regra no município.
6. No Simples Nacional, a alíquota é a efetiva da faixa do prestador, e a retenção é abatida no PGDAS-D.

---

## Fontes

- LC 116/2003 (arts. 3º e 6º) e LC 123/2006 (art. 21, § 4º)
- [Campo tpRetISSQN – NFS-e Nacional](https://buscadorncm.com.br/nfse/tags-xml/tpretissqn)
- [Rejeição E0655](https://buscadorncm.com.br/nfse/erros/e0655)
- [Rejeição E0656 / status da NT 009](https://buscadorncm.com.br/nfse/erros/e0656)
- [Rejeição E0625](https://buscadorncm.com.br/nfse/erros/e0625)
- [Rejeição E0596](https://buscadorncm.com.br/nfse/erros/e0596)
- [Rejeição E1506](https://buscadorncm.com.br/nfse/erros/e1506)
- [Contabilizei – alíquota de retenção no Simples Nacional](https://www.contabilizei.com.br/contabilizei-responde/qual-a-aliquota-de-retencao-de-iss-para-simples-nacional/)
- [Fórum Contábeis – retenção de ISS no Simples (LC 123)](https://www.contabeis.com.br/forum/tributos-estaduais-municipais/84858/retencao-de-iss/)
- [Prefeitura de Franco da Rocha – orientação Simples Nacional](https://www.francodarocha.sp.gov.br/servicos/wp-content/uploads/sites/6/2023/09/simplesnacional.pdf)
