# prompt-config-ai

Repositório com guias em arquivos `.txt` que reúnem **boas práticas de engenharia de prompt** para os modelos **Gemini 2.5 Pro** e **Gemini 2.5 Flash**, aplicados ao contexto de **análise de dados / Data Science**.

---

## Contexto e Performance dos Modelos Gemini

- Os modelos Gemini 2.5 são parte da família de modelos generativos multimodais da Google, disponíveis via **Google AI Studio / API Gemini**. :contentReference[oaicite:0]{index=0}  
- Em aplicações de Data Science, a qualidade da resposta depende fortemente da **engenharia de prompt** (clareza, restrições, contexto).  
- Gemini permite janelas de contexto grandes, mas ainda assim é fundamental controlar delimitações (parâmetro de parada, comprimento máximo etc.). :contentReference[oaicite:1]{index=1}  

---

## Uso da API / AI Studio

Você pode experimentar e prototipar prompts direto em **Google AI Studio** (interface web) e exportar para usar via API. :contentReference[oaicite:2]{index=2}  
A URL para acesso ao AI Studio é:  
[https://aistudio.google.com](https://aistudio.google.com) :contentReference[oaicite:3]{index=3}  

Para chamada via API, algo como (exemplo em Python) pode ser usado:

``` python

import google.generativeai as genai
from dotenv import load_dotenv
import os

load_dotenv()
genai.configure(api_key=os.getenv("GEMINI_API_KEY"))
llm = genai.GenerativeModel(
    model_name="gemini-2.5-flash",
    system_instruction="Seu prompt de sistema aqui"
)
resposta = llm.generate_content("Sua pergunta / prompt aqui")
print(resposta.text)

```
## Parâmetros de Configuração de Prompt
Ao definir prompts para Gemini, você pode controlar diversos parâmetros para ajustar saída, segurança e foco. Aqui estão os principais:
| Parâmetro                                 | Descrição / finalidade                                                                                                                                       |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **temperature**                           | Controle de aleatoriedade. Valores baixos (ex: 0.0 a 0.3) fazem respostas mais determinísticas / seguras; valores mais altos introduzem variação criativa.   |
| **top\_p**                                | Probabilidade cumulativa para truncamento de distribuição (nucleus sampling). Ex: top\_p = 0.9 considera tokens até somar 90% de probabilidade.              |
| **top\_k**                                | Limita o número de tokens candidatos (ex: top\_k = 2 considera os 2 tokens mais prováveis).                                                                  |
| **max\_output\_tokens**                   | Define o comprimento máximo da resposta gerada (em tokens). Limita strings muito longas.                                                                     |
| **response\_mime\_type**                  | Tipo de saída desejada (ex: `"text/plain"`). Pode influenciar formato da resposta.                                                                           |
| **stop\_sequences / sequência de parada** | Tokens ou strings que indicam onde a geração deve parar (ex: `"\n\n"`, `"###"`). Muito útil para estruturar saída controlada.                                |
| **prompt de aterramento / grounding**     | Incluir no prompt informações de apoio ou contexto (“basear resposta em dados reais”, “se for incerto, responda com “Não sei””). Ajuda a evitar alucinações. |
| **saída estruturada**                     | Estruturar o prompt para que a resposta siga formato JSON ou tabela, por exemplo:                                                                            |
``` text
{
 "campo1": "...",
 "campo2": "..."
}

```
## Conteúdo do Repositório
- Arquivos .txt com guias de engenharia de prompt (ex: prompt_gemini_flash.txt, prompt_gemini_pro.txt)
- Exemplos de prompts estruturados e templates
- Instruções gerais sobre contexto, grounding, parâmetros e controle de saída

## Links Úteis & Referências
- Google AI Studio (interface de prototipagem): https://aistudio.google.com
- Documentação Gemini / Developer API: https://ai.google.dev
- Guia introdutório Gemini API + AI Studio: https://developers.google.com/learn/pathways/solution-ai-gemini-101
- Blog sobre melhorias no AI Studio: https://developers.googleblog.com/en/making-it-easier-to-build-with-the-gemini-api-in-google-ai-studio/?utm_source=chatgpt.com
