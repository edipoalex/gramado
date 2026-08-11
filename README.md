# Calculadoras de atrações — Gramado & Canela

Site estático, sem build e sem dependência. Três arquivos:

| Arquivo | O que é |
|---|---|
| `index.html` | Página inicial, com link para as duas calculadoras |
| `individual.html` | Cada pessoa monta a própria lista e vê o próprio gasto |
| `grupo.html` | Soma o custo de todo mundo, com contador de adultos e crianças |

## Publicar no GitHub Pages

### Pelo navegador

1. Em github.com, clique em **New repository**. Nome sugerido: `gramado`. Marque **Public** e crie.
2. Na tela do repositório vazio, clique em **uploading an existing file**.
3. Arraste os três `.html` (não arraste a pasta — arraste os arquivos de dentro dela).
4. Clique em **Commit changes**.
5. Vá em **Settings → Pages**. Em *Source*, escolha **Deploy from a branch**. Em *Branch*, escolha **main** e a pasta **/ (root)**. Clique em **Save**.
6. Espere de 1 a 2 minutos e recarregue a página de Settings → Pages. O link aparece no topo:

```
https://SEU-USUARIO.github.io/gramado/
```

### Pelo terminal

```bash
git init
git add index.html individual.html grupo.html
git commit -m "Calculadoras de atrações de Gramado e Canela"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/gramado.git
git push -u origin main
```

Depois ative em **Settings → Pages**, com *Deploy from a branch*, branch `main`, pasta `/ (root)`.

## Atualizar os preços depois

Os valores ficam no array `ATRACOES`, dentro do `<script>` de cada calculadora.

Atenção no `individual.html`: a lista também está escrita direto no HTML, dentro de `<div id="lista">`, para a página funcionar mesmo sem JavaScript. Ao editar o array, esse trecho fica desatualizado até a página carregar e reescrevê-lo. Quem abrir com JavaScript ligado — ou seja, todo mundo no navegador — vê sempre o valor novo.

## Detalhes de implementação

- Zero dependência de runtime. A única requisição externa é o Google Fonts, e a página degrada para fontes do sistema se ele não carregar.
- A seleção é gravada no fragmento da URL (`#adulto~snowland,minimundo`), então dá para mandar um link já com o roteiro montado. Em `file://` isso falha em silêncio, porque a origem é nula.
- Nenhum dado sai do dispositivo. Não há backend, cookie nem analytics.
