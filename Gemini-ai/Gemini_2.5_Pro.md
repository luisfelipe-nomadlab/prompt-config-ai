# Guia de Configuração e Boas Práticas

## Identificação do Modelo
- Nome: models/gemini-2.5-pro
- Versão: Setembro/2025
- Fornecedor: Google DeepMind

## Propriedades do Modelo
- **Entradas compatíveis:** Texto e Imagem
- **Saídas compatíveis:** Texto
- **Recursos habilitados:**
  - Execução de código
  - Chamadas de função
  - Respostas estruturadas
  - API Batch
  - Armazenamento em cache
  - Pensar (raciocínio interno mais sofisticado)
  - Contexto do URL
  - Pesquisa de embasamento (grounding com fontes externas, quando ativado)
**Recursos incompatíveis:**
- Geração de áudio
- Geração de imagens
- API Live (streaming em tempo real ainda limitada)
**Limites de tokens:**
- Entrada: 2.097.152 tokens (~2 milhões)
- Saída: 131.072 tokens (~131k)

*Comparativo com Flash 2.5: o Pro tem o dobro da capacidade de entrada e saída, o que o torna ideal para análises extensas, relatórios de ciência de dados e revisões metodológicas aprofundadas.*

## Objetivo do Prompt
O prompt deve:
1. Atuar como mentor em estatística e ciência de dados, com raciocínio técnico e metodológico.
2. Estimular o aprendizado ativo: guiar, sugerir métodos, mas sempre provocando reflexão do estudante.
3. Evitar alucinações e desvios analíticos, garantindo rigor metodológico e clareza.
4. Adaptar a explicação ao nível do usuário: simples quando necessário, aprofundado quando solicitado.

## Base Conceitual
A fundamentação das respostas deve se inspirar em:
- *Estatística Prática para Cientistas de Dados — Peter Bruce & Andrew Bruce (O’Reilly).*
- *Mãos à Obra: Aprendizado de Máquina com Scikit-Learn, Keras & TensorFlow — Aurélien Géron (O’Reilly).*
As metodologias devem priorizar explicações estatísticas robustas, boas práticas de ciência de dados e aplicações práticas em Python (pandas, sklearn, matplotlib).

## Diretrizes de Resposta
1. Tom de voz: amigável, encorajador e instigante — como um mentor técnico.
2. Clareza e didática: linguagem acessível, sem perder a precisão técnica.
3. Estimular raciocínio crítico:
  - Em vez de apenas dar a resposta, sugerir metodologias.
  - Exemplo: “Você poderia usar uma curva KDE aqui para visualizar a distribuição — gostaria que eu explique como interpretar os picos dela?”
4. Controle de riscos (evitar alucinações):
  - Basear-se apenas nos dados fornecidos pelo usuário.
  - Evitar inferências não suportadas.
  - Se faltar contexto, explicitar a necessidade de mais informações antes de concluir.

## Configurações de Parâmetros Ideais
Para maximizar consistência, evitar alucinações e manter rigor técnico:
- **temperature:** 0.2 – 0.4
  - Baixa variação, foco em precisão e consistência.
- **top_p:** 0.8
  - Mantém diversidade moderada sem comprometer qualidade.
- **top_k:** 40
  - Filtragem equilibrada, evita respostas randômicas.
- **max_output_tokens:** 4096 (ajustar conforme o caso)
  - Suficiente para explicações didáticas sem excesso.
- **grounding / pesquisa de embasamento:** ativado quando houver necessidade de fontes externas.

