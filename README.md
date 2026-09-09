# Gramado & Canela — roteiro e calculadoras

Site estático, sem build e sem dependência. No ar em:

**https://edipoalex.github.io/gramado/**

| Arquivo | O que é |
|---|---|
| `index.html` | Home, com os links para o roteiro e para as duas calculadoras |
| `roteiro.html` | Roteiro dia a dia da viagem, 26/10 a 04/11/2027 |
| `individual.html` | Cada pessoa monta a própria lista e vê o próprio gasto |
| `grupo.html` | Soma o custo de todo mundo, com contador de adultos e crianças |

Todas as páginas internas voltam para a home pelo link `← Início` no topo.

## Atualizar o site

```bash
git add -A
git commit -m "descrição da mudança"
git push
```

O GitHub Pages reconstrói sozinho em cerca de um minuto. A configuração é *Deploy from a branch*, branch `main`, pasta `/ (root)`.

## Atualizar os preços

Os valores ficam no array `ATRACOES`, dentro do `<script>` de cada calculadora.

Atenção no `individual.html`: a lista também está escrita direto no HTML, dentro de `<div id="lista">`, para a página funcionar mesmo sem JavaScript. Ao editar o array, esse trecho fica desatualizado até a página carregar e reescrevê-lo. Quem abrir com JavaScript ligado — ou seja, todo mundo no navegador — vê sempre o valor novo.

## Atualizar o roteiro

O `roteiro.html` é HTML escrito à mão, sem script. Cada dia é um `<article class="dia ...">`, onde a classe define a cor da borda: `gramado`, `canela`, `bento`, `semcarro` ou `estrada`. Dentro, cada item é um `<li class="it ...">` com `att` (atração), `meal` (refeição), `drive` (deslocamento) ou `livre`.

## Detalhes de implementação

- Zero dependência de runtime. A única requisição externa é o Google Fonts, e as páginas degradam para fontes do sistema se ele não carregar.
- Nas calculadoras, a seleção é gravada no fragmento da URL (`#adulto~snowland,minimundo`), então dá para mandar um link já com o roteiro montado. Em `file://` isso falha em silêncio, porque a origem é nula.
- O `roteiro.html` tem estilo de impressão: os dias não quebram no meio da página e os links de perfil somem.
- Nenhum dado sai do dispositivo. Não há backend, cookie nem analytics.
