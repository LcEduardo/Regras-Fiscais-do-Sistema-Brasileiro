# Remessa de Mercadoria e CFOP 5.949

Remessa é a saída de mercadoria **sem transferência de propriedade** (ou sem venda): a mercadoria circula, mas não é vendida. O ICMS **não segue uma regra única** — ele depende do motivo da remessa e do que a legislação da UF prevê para aquela operação.

Regra de ouro: **"remessa" não significa "sem ICMS"**. Sem isenção, suspensão ou não incidência prevista em lei, o ICMS é destacado normalmente.


## Fundamento legal

• Convênio SINIEF s/n, de 1970 — regras de emissão de documentos fiscais, incluindo a venda à ordem.
• Súmula 573 do STF — não incidência do ICMS na saída em comodato.
• Convênio ICMS 129/2006 — remessa de peça defeituosa em garantia (conferir adesão e condições na UF).
• RICMS de cada UF — suspensão (conserto, industrialização, demonstração) e demais benefícios.


## Remessa por conta e ordem (venda à ordem) — CFOP 5.923 / 6.923

Usada quando a mercadoria é entregue fisicamente a um destinatário diferente de quem comprou (ex.: o adquirente originário vende para um terceiro e pede para o vendedor entregar direto).

| Nota | Quem emite | CFOP | ICMS |
|---|---|---|---|
| Faturamento ao adquirente originário | Vendedor remetente | 5.118 / 5.119 (6.118 / 6.119) | **Destacado** |
| Remessa ao destinatário final | Vendedor remetente | **5.923 / 6.923** | **Sem destaque** |
| Venda do adquirente originário ao destinatário | Adquirente originário | 5.120 / 6.120 | **Destacado** |

Na nota de remessa (5.923 / 6.923):
• `finNFe = 1` (normal).
• Sem destaque de ICMS — o imposto está nas notas de faturamento. Não gera crédito nem débito.
• CST sem valores de ICMS (usualmente 90 ou 41, conforme orientação da UF).
• Informações complementares: número, série e data da nota de faturamento e identificação do adquirente originário.
• Pode referenciar a nota de faturamento em `NFref`.

Junto com uma devolução: a NF-e de devolução (ex.: 5.202) mantém o ICMS calculado normalmente (ver `devolução.md`); a remessa 6.923 só acoberta a entrega física e sai sem ICMS.


## Outras remessas e seus retornos

| Remessa | CFOP | Retorno | ICMS |
|---|---|---|---|
| Conserto ou reparo | 5.915 / 6.915 | 5.916 / 6.916 | Suspensão (CST 50), conforme RICMS da UF |
| Industrialização por encomenda | 5.901 / 6.901 | 5.902 / 6.902 | Suspensão (CST 50), conforme RICMS da UF |
| Demonstração | 5.912 / 6.912 | 5.913 / 6.913 | Suspensão ou isenção, conforme a UF |
| Comodato | 5.908 / 6.908 | 5.909 / 6.909 | Não incidência (CST 41) |
| Bonificação, doação ou brinde | 5.910 / 6.910 | — | **Tributada normalmente** |
| Amostra grátis | 5.911 / 6.911 | — | Isenção condicionada, conforme a UF |

• **O retorno acompanha a remessa**: se a ida saiu com suspensão, o retorno também sai com suspensão.
• Suspensões costumam ter **prazo para o retorno** (definido no RICMS da UF). Vencido o prazo sem retorno, o ICMS passa a ser devido.


## CFOP 5.949 / 6.949 — Outra saída não especificada

CFOP residual: **"Outra saída de mercadoria ou prestação de serviço não especificado"**. Só deve ser usado quando **nenhum outro CFOP** descreve a operação.

### ICMS no 5.949

O CFOP não define o imposto. O padrão é **destacar o ICMS**:

• **Existe isenção, suspensão ou não incidência prevista em lei para a operação?**
  - **Sim** → sem destaque, com o CST correspondente (40, 41, 50 ou 90) e o dispositivo legal nas informações complementares.
  - **Não** → **destaca o ICMS** (CST 00 / CSOSN 900), como em uma venda.

### Regras de uso

• Não usar o 5.949 quando existir CFOP específico (devolução, conserto, bonificação etc.) — o uso indevido pode gerar autuação.
• `natOp` deve descrever a operação real (ex.: "Remessa de peça em garantia", "Doação") — evitar "Outras saídas".
• Informações complementares devem explicar a operação e, se não houver destaque, citar a base legal do benefício.
• Normalmente não gera receita: conferir se o sistema não está tratando a nota como faturamento.

### Exemplos

| Operação | Destaca ICMS? | Motivo |
|---|---|---|
| Remessa de peça defeituosa ao fabricante, em garantia | Em regra **não** | Isenção do Convênio ICMS 129/2006 (conferir UF) |
| Doação | **Sim** | Em regra não há benefício |
| Remessa para troca | Depende | Varia conforme a UF |

### Erro mais comum

Tratar o 5.949 como "CFOP sem imposto" e zerar o ICMS sem base legal. Isso gera ICMS não recolhido e risco de autuação. **Sem dispositivo que dê o benefício, destaque o imposto.**


## Ver também

• Regras de devolução: `2 - Regras/devolução.md`.
• Processo interno (devolução + remessa): `processos/Emissao_fiscal_devolucao`.
