# Se a Câmara realmente representasse o Brasil?

Análise do **Desvio Padrão ([@desviopadrao.info](https://www.instagram.com/desviopadrao.info/))** que compara os **513 deputados federais eleitos em 2026** (legislatura 2027–2031) com a população brasileira do **Censo 2022** em gênero, cor/raça, idade, escolaridade e ocupação. Inclui a "Câmara proporcional" (como seriam as cadeiras se espelhassem a população), a evolução 2018–2026 e o funil de candidatos a eleitos.

## Conteúdo

| Arquivo | Descrição |
|---|---|
| [`analise_camara_representatividade.ipynb`](analise_camara_representatividade.ipynb) | Notebook completo: download, validações, harmonização das categorias TSE × IBGE, métricas e exportação |
| [`output/`](output/) | Um JSON por gráfico do post; [`metodologia.json`](output/metodologia.json) traz fontes e notas metodológicas |
| `requirements.txt` | Pacotes Python usados |

Os dados brutos (`dados/`) **não ficam no repositório**: o notebook baixa das fontes oficiais e guarda em cache na primeira execução.

## Fontes

- **TSE**: candidaturas de 2018, 2022 e 2026 (`consulta_cand`), [Portal de Dados Abertos do TSE](https://dadosabertos.tse.jus.br/).
- **IBGE, Censo Demográfico 2022** via [SIDRA](https://sidra.ibge.gov.br): tabelas 9606 (cor ou raça, sexo e idade), 10061 (nível de instrução) e 10264 (grandes grupos de ocupação).

## Como rodar

Requisitos: Python 3.12 e Jupyter.

```bash
python -m venv .venv
pip install -r requirements.txt
jupyter notebook analise_camara_representatividade.ipynb
```

Rode com **Restart Kernel & Run All**. Os downloads vão para `dados/` (só baixa se o arquivo não existir) e os JSONs vão para `output/` e para a pasta do post no gerador de conteúdo (`../desviopadrao-slides/src/posts/2026-11-a-camara-parece-com-o-brasil/dados/`), que é criada se não existir.

## Pontos de atenção

- Gênero, cor/raça e ocupação são **autodeclarados** no registro de candidatura (TSE) e no Censo.
- Comparações usam populações diferentes conforme o tema: total para gênero e cor/raça, 18+ para idade, 25+ para escolaridade.
- As 7 categorias de instrução do TSE foram agrupadas nos 4 níveis do Censo; a ocupação usa um **mapeamento próprio** da lista do TSE para os grandes grupos da COD (não há tabela oficial de correspondência).
- A Câmara proporcional distribui as 513 cadeiras pelo método dos maiores restos (Hamilton).

A lista completa está em [`output/metodologia.json`](output/metodologia.json) e nas células do notebook.

## Licença

[MIT](LICENSE) © 2026 Desvio Padrão
