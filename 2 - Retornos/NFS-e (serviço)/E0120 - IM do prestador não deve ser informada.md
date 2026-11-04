# E0120 — Inscrição Municipal do prestador não deve ser informada

**Documento:** NFS-e (serviço) — Padrão Nacional (DPS)
**Código de retorno:** E0120 (par oposto: E0116)
**Mensagem do Sistema Nacional NFS-e:**

```
E0120 - A IM não deve ser informada para o emitente prestador do serviço na DPS
```

> ⚠️ Mensagem reproduzida conforme relatos de provedores. Ao receber a rejeição em produção, cole aqui o texto exato do retorno.

Voltar para: [[MOC - Retornos]]


## Contexto

Com a migração das empresas do **Simples Nacional** para o **ambiente nacional da NFS-e** (relato interno: obrigatório a partir de **01/11/2026** — ⚠️ confirmar a base legal com a contabilidade antes de citar como regra), muitos clientes que antes emitiam pelo webservice da prefeitura (ABRASF), onde a IM era obrigatória, passam a enviar a DPS ao Sistema Nacional.

No ambiente nacional, **quem decide se a IM vai ou não no XML é o cadastro do município no CNC** (Cadastro Nacional de Contribuintes), não o sistema emissor.


## Causa

A tag `prest/IM` foi enviada na DPS, mas o município emissor (`cLocEmi`) **não tem informações complementares no CNC**. Nesse caso o Sistema Nacional identifica o prestador **só pelo CNPJ/CPF** e rejeita a IM.

| Situação do município no CNC | `prest/IM` na DPS | Resultado |
|---|---|---|
| Sem informações complementares no CNC | Enviada | ❌ **E0120** — IM não deve ser informada |
| Sem informações complementares no CNC | Não enviada | ✅ Autoriza |
| Com cadastro complementar no CNC (ex.: São Luís/MA) | Não enviada | ❌ **E0116** — IM deve ser informada |
| Com cadastro complementar no CNC | Enviada, mas não existe/inativa | ❌ **E043 / E0124** — IM não encontrada ou inativa |
| Com cadastro complementar no CNC | Enviada e válida | ✅ Autoriza |

Ou seja: **não dá para tratar como "nunca enviar a IM"**. A regra é por município.


## Exemplo do XML rejeitado

```xml
<prest>
  <CNPJ>12345678000199</CNPJ>
  <IM>123456</IM>          <!-- município sem CNC complementar: remover -->
  <regTrib>
    <opSimpNac>3</opSimpNac>
    <regApTribSN>1</regApTribSN>
    <regEspTrib>0</regEspTrib>
  </regTrib>
</prest>
```

XML corrigido (mesmo caso):

```xml
<prest>
  <CNPJ>12345678000199</CNPJ>
  <regTrib>
    <opSimpNac>3</opSimpNac>
    <regApTribSN>1</regApTribSN>
    <regEspTrib>0</regEspTrib>
  </regTrib>
</prest>
```


## Como resolver

1. Confirmar o município emissor (`cLocEmi`) da nota.
2. **Remover a tag `prest/IM`** do XML da DPS (no sistema: não enviar a IM para esse município no Padrão Nacional). Manter a IM no cadastro da empresa — ela continua sendo usada em outros documentos e se o município passar a exigir.
3. Reenviar a DPS.
4. Se depois disso vier **E0116**, o município exige a IM: voltar a enviar e conferir se ela está ativa no cadastro da prefeitura.


## Impacto no sistema (sugestão)

• Tornar o envio da `prest/IM` **configurável por município** no Padrão Nacional (padrão: **não enviar**), em vez de sempre enviar a IM do cadastro da empresa.
• Registrar aqui os municípios que exigem a IM (E0116) conforme forem aparecendo.

| Município | Exige IM no Padrão Nacional? | Fonte |
|---|---|---|
| São Luís (MA) | Sim (E0116) | Relato de terceiros — confirmar |


## Fontes

• [Fiscal Contora — Rejeições E0116 e E0120 (IM e CNC)](https://fiscal.contora.com.br/blog/nfse-nacional-rejeicoes-e0116-e0120-inscricao-municipal-cnc)
• [NFe-Mail — E0116: a IM deve ser informada](https://suporte.nfemail.com.br/kb/pt-br/article/598948/e0116-rejeicao-a-im-deve-ser-informada-para-o-emitente-prestador)
• [Tecnospeed — E043: IM do prestador não encontrada](https://atendimento.tecnospeed.com.br/hc/pt-br/articles/36608422894487-NFS-e-Como-resolver-a-Rejei%C3%A7%C3%A3o-E043-Inscri%C3%A7%C3%A3o-Municipal-do-prestador-n%C3%A3o-encontrada-Padr%C3%A3o-Nacional)
• Oficial: Anexo de regras de negócio da DPS no [Portal NFS-e Nacional](https://www.gov.br/nfse) — ⚠️ conferir os códigos e mensagens na versão vigente.

Relacionados: [[NFS-e (serviço)]]
