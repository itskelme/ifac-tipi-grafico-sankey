# Gráficos Sankey com Google Charts

> Duas páginas HTML que desenham diagramas de Sankey com o Google Charts para visualizar como categorias de um levantamento se distribuem.

**Contexto:** IFAC · Técnico em Informática para Internet (TIPI) · 3º ano · 2023

## Sobre

Um diagrama de Sankey mostra fluxos entre categorias: cada faixa liga uma origem a um destino, e a largura da faixa é proporcional ao valor. O projeto usa o pacote `sankey` do Google Charts, a partir do exemplo do guia oficial, e adapta os dados para dois levantamentos:

- `index.html`: tecnologias imersivas (AR, VR, MR) → tipo de conteúdo → tipo de affordance → finalidade, em quatro colunas.
- `rege.html`: objetivos de pesquisas sobre Pensamento Computacional (PC) → nível de ensino em que foram aplicadas.

O objetivo foi aprender a montar um `DataTable` no formato origem/destino/peso, carregar o Google Charts e ajustar as opções do gráfico.

## Funcionalidades

### `index.html`: tecnologias imersivas e affordances

Quatro níveis ligados em sequência:

1. **Tecnologia:** AR, VR, MR
2. **Tipo:** Static, Dynamic
3. **Affordance:** Visual, Sound, Hapitic (escrito assim no código)
4. **Finalidade:** Learning, Interaction, Mounting, Navigation

Alguns pesos são escritos como somas (por exemplo, `0.5 + 0.5 + 1`), o que deixa visível de onde veio cada valor. Opções: 900 × 240 px e `nodePadding: 20`.

### `rege.html`: Pensamento Computacional por nível de ensino

Liga seis objetivos ("Desenvolver habilidades do PC", "Promover o ensino de PC", "Desenvolver o raciocínio lógico e habilidades de programação", "Resolver problemas", "Promover a inclusão", "Avaliar práticas de ensino") aos níveis Infantil, Fundamental, Médio, Médio Técnico e Superior. Os nós e as faixas são todos cinza (`#aaaaaa`). Opções: 900 × 640 px e `nodePadding: 20`.

Nos dois gráficos, passar o mouse sobre uma faixa mostra a origem, o destino e o peso (comportamento padrão do Google Charts).

## Tecnologias

- HTML
- JavaScript
- [Google Charts](https://developers.google.com/chart) (pacote `sankey`, carregado de `https://www.gstatic.com/charts/loader.js`)

## Estrutura do projeto

| Caminho | Descrição |
|---|---|
| `index.html` | Sankey de tecnologias imersivas, tipos, affordances e finalidades. |
| `rege.html` | Sankey de objetivos de Pensamento Computacional por nível de ensino. |

## Como rodar

### Pré-requisitos

- Um navegador
- Conexão com a internet (a biblioteca do Google Charts é baixada na hora)

### Passo a passo

```bash
git clone https://github.com/itskelme/ifac-tipi-grafico-sankey.git
cd ifac-tipi-grafico-sankey
```

Abra `index.html` ou `rege.html` direto no navegador. Se preferir servir por HTTP:

```bash
python -m http.server 8000
# ou: php -S localhost:8000
```

E acesse http://localhost:8000/index.html ou http://localhost:8000/rege.html

## Como usar

Para trocar os dados, edite o array dentro de `data.addRows([...])`. Cada linha é `[origem, destino, peso]`:

```js
data.addRows([
  ["AR", "Static", 5],
  ["Static", "Visual affordances", 4.5],
]);
```

Um nó que aparece como destino numa linha e como origem em outra cria uma nova coluna no gráfico. O Google Charts não aceita ciclos (A → B → A). Tamanho, espaçamento e cores ficam no objeto `options` passado para `chart.draw(data, options)`.

## Observações

- A `div` do gráfico tem 2000 × 900 px no estilo, mas o desenho usa o `width`/`height` das opções, então sobra espaço em branco.
- Em `rege.html`, a ligação "Promover o ensino de PC" → "Infantil" tem peso 0, por isso não gera faixa visível.

## Referências

- [Google Charts: Sankey Diagram](https://developers.google.com/chart/interactive/docs/gallery/sankey)
- [Google Charts: carregando a biblioteca](https://developers.google.com/chart/interactive/docs/basic_load_libs)
- [Google Charts: `DataTable`](https://developers.google.com/chart/interactive/docs/reference#DataTable)

## Autores

- Diego Kelme Santos da Silva — [@itskelme](https://github.com/itskelme)

## Licença

Este projeto está sob a licença [CC BY-NC 4.0](LICENSE): uso pessoal e modificação permitidos com atribuição; uso comercial proibido.
