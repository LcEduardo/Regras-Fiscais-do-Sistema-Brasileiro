# 225 — Falha no Schema XML (cEAN inválido)

**Documento:** NFC-e (modelo 65)
**Código de retorno (cStat):** 225
**Mensagem da SEFAZ:**

```
Rejeicao: Falha no Schema XML da NFe (Elemento: enviNFe/NFe[1]/infNFe/det[1]/prod/cEAN)
```

> A mensagem cita `enviNFe/NFe` porque a NFC-e usa o mesmo leiaute de XML da NF-e. O que diferencia os dois é o modelo (`<mod>65</mod>`).

Voltar para: [[MOC - Retornos]]
Tags envolvidas: `cEAN` e `cEANTrib` em [Layout XML — NFC-e](../../4%20-%20Layout%20XML/NFC-e%20(modelo%2065).md)


## Causa

O campo `cEAN` (código de barras do produto) foi enviado com um valor que não é um código de barras válido. No exemplo abaixo, o sistema enviou o **código interno do produto** (`1123`) no lugar do código de barras.

O campo `cEAN` só aceita:
• Um GTIN válido (EAN-8, EAN-13, GTIN-12 ou GTIN-14), com a quantidade de dígitos correta; ou
• O texto `SEM GTIN`, quando o produto não possui código de barras.

O valor `1123` tem apenas 4 dígitos, por isso o XML é recusado já na validação do schema.

> O mesmo problema costuma acontecer no campo `cEANTrib` (código de barras da unidade tributável), que segue as mesmas regras.


## Exemplo do XML rejeitado

```xml
<det nItem="1">
<prod>
<cProd>1123</cProd>
<cEAN>1123</cEAN>
<xProd>FUSIVEL MINI 10A LAMINA</xProd>
<NCM>85361000</NCM>
<CFOP>5102</CFOP>
<uCom>UN</uCom>
<qCom>1.0000</qCom>
<vUnCom>1.5000000000</vUnCom>
<vProd>1.50</vProd>
<cEANTrib>1123</cEANTrib>
<uTrib>UN</uTrib>
<qTrib>1.0000</qTrib>
<vUnTrib>1.5000000000</vUnTrib>
<indTot>1</indTot>
</prod>
<imposto>
<vTotTrib>0.49</vTotTrib>
<ICMS>
<ICMSSN102>
<orig>0</orig>
<CSOSN>102</CSOSN>
</ICMSSN102>
</ICMS>
<PIS>
<PISNT>
<CST>07</CST>
</PISNT>
</PIS>
<COFINS>
<COFINSNT>
<CST>07</CST>
</COFINSNT>
</COFINS>
</imposto>
</det>
```


## Como resolver

1. No cadastro do produto, verificar o campo de código de barras / EAN.
2. Se o produto tiver código de barras, informar o GTIN correto (8, 12, 13 ou 14 dígitos).
3. Se o produto **não** tiver código de barras, deixar o campo vazio no cadastro, para que o sistema envie `SEM GTIN`.
4. Conferir se o código interno do produto não foi digitado no campo de código de barras.
5. Reenviar a nota.
