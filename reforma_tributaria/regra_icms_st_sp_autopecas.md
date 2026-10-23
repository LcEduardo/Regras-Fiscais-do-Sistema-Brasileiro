# ICMS-ST em São Paulo 2026: resumo e referências

*Elaborado em 29/09/2026 para uso interno (ERP de oficinas mecânicas). Não é consultoria tributária: valide com a contabilidade e com o texto oficial antes de alterar regras fiscais no sistema.*

---

## 1. Resumo executivo

- **Portaria SRE nº 34/2026** (assinada em 29/06/2026 e publicada no DOE-SP em 30/06/2026) retira cerca de **174 mercadorias** da substituição tributária do ICMS em SP, com vigência em **01/10/2026**.
- Segmentos com **exclusão total**: **autopeças** (Anexo XIV), **pneumáticos, câmaras de ar e protetores de borracha** (Anexo VII), tintas e vernizes (Anexo VIII), ferramentas (Anexo XVIII) e materiais elétricos (Anexo XXI).
- Exclusão **parcial** adicional: CEST 21.002.00 a 21.010.00 e 21.015.00 de eletroeletrônicos (Anexo XXII).
- Também revoga as portarias que fixavam a base de cálculo (IVA-ST/MVA) desses segmentos, entre elas a SRE 16/2023 (autopeças) e a SRE 15/2024 (pneumáticos).
- O **estoque** existente em 30/09/2026 deve seguir a **Portaria CAT 28/2020** (art. 2º da Portaria SRE 34/2026): inventário, escrituração na EFD (Bloco H) e apuração do crédito.
- Não confundir com a onda anterior (Portarias **SRE 19/2026 e 20/2026**, vigência em **01/08/2026**), que retirou 47 itens de materiais de construção, eletrônicos, ração pet e limpeza.

## 2. Linha do tempo

| Data | Fato |
|---|---|
| 01/01/2026 | Só o CEST 01.015.00 (vidros automotivos) sai da ST de autopeças |
| 30/04 e 05/05/2026 | Publicadas as Portarias SRE 19 e 20/2026 |
| 29–30/06/2026 | Assinada e publicada a Portaria SRE 34/2026 |
| 01/08/2026 | Entram em vigor as Portarias SRE 19 e 20/2026 |
| 14–15/09/2026 | CONFAZ celebra e divulga os Protocolos ICMS 93, 94 e 96/2026 (Despacho CONFAZ 43/2026) |
| **30/09/2026** | **Data-base do inventário de estoque** |
| **01/10/2026** | **Vigência da Portaria SRE 34/2026** |

## 3. Impacto prático no ERP

1. **Vigência por data de emissão**: notas até 30/09/2026 seguem a regra antiga; a partir de 01/10/2026, tributação normal.
2. **Cadastro fiscal dos itens afetados**: revisar CST/CSOSN (saída de CST 60 / CSOSN 500 e derivados de ST), CFOP (por exemplo, 5.405 → 5.102 nas vendas internas) e campos de MVA/base ST/ICMS-ST.
3. **CEST permanece na NF-e**, mesmo sem ST (Convênio ICMS 142/2018, cláusula 20).
4. **Entradas**: fornecedores paulistas deixam de destacar ICMS-ST nos itens afetados, o que altera custo e crédito.
5. **Vendas interestaduais**: os Protocolos ICMS 93, 94 e 96/2026 encerram os acordos de autopeças de SP. Revisar DIFAL, GNRE e regras do destino (segundo a JJR Contabilidade).
6. **Estoque**: gerar relatório por NCM/CEST/quantidade/valor em 30/09/2026 para o contador.
7. **Devoluções e cancelamentos** de notas anteriores a 01/10 podem exigir a regra antiga.

## 4. Pontos de atenção e divergências entre fontes

- O guia da Tributei cita o **Anexo VII** para autopeças em um trecho. Outras fontes (ABREME, 3S Corp, MG Contécnica, Martinelli) indicam **Anexo XIV = autopeças** e **Anexo VII = pneumáticos**.
- A lista de 125 itens de autopeças usada na planilha vem de artigo da JJR Contabilidade. Não é o texto oficial.
- Lubrificantes e fluidos não constam dos segmentos revogados nas fontes consultadas.
- Blogs de software e de contabilidade podem ter viés comercial. Prevalece o texto da portaria.

---

## 5. Referências

### 5.1 Legislação oficial (SEFAZ/SP)

- [Portaria SRE nº 34/2026](https://legislacao.fazenda.sp.gov.br/Paginas/Portaria-SRE-34-de-2026.aspx)
- [Portaria CAT nº 68/2019 (consolidada), relação de mercadorias sujeitas à ST](https://legislacao.fazenda.sp.gov.br/Paginas/Portaria-CAT-68-de-2019.aspx)
- [Portaria CAT nº 28/2020, tratamento do estoque](https://legislacao.fazenda.sp.gov.br/Paginas/Portaria-CAT-28-de-2020.aspx)
- [Portaria SRE nº 19/2026](https://legislacao.fazenda.sp.gov.br/Paginas/Portaria-SRE-19-de-2026.aspx) e [Portaria SRE nº 20/2026](https://legislacao.fazenda.sp.gov.br/Paginas/Portaria-SRE-20-de-2026.aspx) (onda de agosto)
- [Compilação de convênios e protocolos de ST firmados por SP](https://legislacao.fazenda.sp.gov.br/Paginas/ConveniosProtocolosSubstituicaoTributaria.aspx)

### 5.2 CONFAZ (operações interestaduais)

- [Despacho CONFAZ nº 43/2026 (Protocolos ICMS 90 a 123/2026)](https://www.confaz.fazenda.gov.br/legislacao/despacho/2026)
- [Protocolo ICMS nº 41/2008 (autopeças)](https://www.confaz.fazenda.gov.br/legislacao/protocolos/2008/pt041_08)
- [Convênio ICMS nº 142/2018](https://www.confaz.fazenda.gov.br/legislacao/convenios/2018/CV142_18)

### 5.3 Texto e análises da Portaria SRE 34/2026

- [LegisWeb: Portaria SRE 34/2026](https://www.legisweb.com.br/legislacao/?id=497430)
- [ABREME: transcrição da portaria (material elétrico)](https://abreme.com.br/?p=6750)
- [Martinelli Advogados: nova exclusão de mercadorias da ST](https://www.martinelli.adv.br/sao-paulo-promove-nova-exclusao-de-mercadorias-do-regime-de-substituicao-tributaria/)
- [Senior: Fim do ICMS-ST em SP para diversos segmentos](https://documentacao.senior.com.br/exigenciaslegais/noticias/estadual/2026/2026-07-02-icms-sp-portaria-sre-no-34-2026-fim-do-icms-substituicao-tributaria-em-sao-paulo-para-diversos-segmentos/)
- [Consystem: Portaria SRE 34/2026 e autopeças](https://consystem.com.br/pt/a-portaria-sre-no-34-2026-de-sao-paulo-revoga-varios-segmentos-entre-elas-autopecas-da-sistematica-da-substituicao-tributaria-a-partir-de-01-10-2026/)
- [3S Corp: guia técnico (125 itens de autopeças, 19 de ferramentas etc.)](https://www.3scorporate.com/icms-st-sp/)
- [ERPFlex: guia de parametrização (NCMs 4011, 4012, 4013)](https://docsnew.erpflex.com.br/portaria-sre-34-2026/)
- [Omie: 174 mercadorias saem do ICMS-ST](https://www.omie.com.br/blog/governo-sp-exclui-174-mercadorias-icms-st/)
- [MG Contécnica: pneumáticos, câmaras de ar e protetores](https://mgcontecnica.com.br/2026/09/29/reforco-de-comunicado-estado-de-sao-paulo-exclui-pneumaticos-camaras-de-ar-e-protetores-de-borracha-da-substituicao-tributaria-a-partir-de-1o-10-2026-2/)

### 5.4 Autopeças: interestadual, DIFAL e lista de itens

- [JJR Contabilidade: ICMS-ST de autopeças, protocolos 93/94/96 e tabela dos 125 itens](https://jjrcontabil.com.br/icms-st-autopecas-2026-sao-paulo/)
- [Tributei: exclusão de outubro (autopeças, materiais elétricos, ferramentas)](https://tributei.net/blog/exclusao-icms-st-sp-outubro-2026/)

### 5.5 Contexto geral das exclusões em 2026

- [Tributei: ICMS-ST 2026 em SP, guia completo das cinco ondas](https://tributei.net/blog/icms-st-2026-sao-paulo/)
- [FecomercioSP: Sefaz/SP exclui 47 itens do ICMS-ST (onda de agosto)](https://www.fecomercio.com.br/noticia/sefaz-sp-exclui-47-itens-do-icms-st-e-da-mais-um-passo-a-desburocratizacao-do-sistema-tributario)
- [FecomercioSP: lista dos 47 itens excluídos (.docx)](https://lab.fecomercio.com.br/wp-content/uploads/2026/05/Produtos_excluidos_ICMS_ST.docx)

---

## 6. Checklist rápido para o time

- [ ] Confirmar o texto oficial da Portaria SRE 34/2026 e os anexos VII, VIII, XIV, XVIII e XXI da CAT 68/2019
- [ ] Cruzar NCM/CEST da base de produtos com a planilha `ICMS-ST_SP_Autopecas_Pneus_Saida_01-10-2026.xlsx`
- [ ] Configurar vigência por data de emissão (regra antiga até 30/09, normal a partir de 01/10)
- [ ] Revisar CST/CSOSN, CFOP e campos de ST nos itens afetados, sem apagar códigos globalmente
- [ ] Manter o CEST no cadastro e na NF-e
- [ ] Revisar regras de entrada (fornecedores paulistas e interestaduais)
- [ ] Revisar DIFAL e GNRE nas vendas interestaduais de autopeças
- [ ] Gerar relatório de estoque de 30/09/2026 por NCM/CEST para a contabilidade (Portaria CAT 28/2020)
- [ ] Comunicar os clientes (oficinas) e o intermediador sobre a virada
- [ ] Validar tudo com o contador