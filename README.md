# Gramado & Canela 2027 — site da viagem

Site estático, sem build e sem dependência. No ar em:

**https://edipoalex.github.io/gramado/**

Tudo fica numa página só, `index.html`, com três abas:

| Aba | Endereço | O que mostra |
|---|---|---|
| Roteiro | `#roteiro` | Os 11 dias, de 25/10 a 04/11/2027, com horário, preço, custo do dia e link para o mapa |
| Gastos | `#gastos` | Hospedagem, passagens e atrações por família e do grupo |
| Calculadora | `#calculadora` | Marca e desmarca atrações e mostra o total para quem você escolher |

Também dá para abrir um dia direto: `#dia-2027-10-28`.

As páginas antigas (`roteiro.html`, `individual.html` e `grupo.html`) só redirecionam para a aba certa. Assim os links que já circularam no grupo continuam funcionando.

## Atualizar o site

```bash
git add -A
git commit -m "descrição da mudança"
git push
```

O GitHub Pages reconstrói sozinho em cerca de um minuto. A configuração é *Deploy from a branch*, branch `main`, pasta `/ (root)`.

## Onde mudar as coisas

Tudo que muda está no começo do `<script>` do `index.html`, em três listas:

- **`ATRACOES`**: o preço de cada atração, e em `ig` o perfil oficial no Instagram (conferido em 23/11/2026). `ad` e `cd` são os preços com desconto de adulto e criança, e `ac` e `cc` os preços cheios. Mudando aqui, mudam juntos o roteiro, o custo de cada dia, a aba Gastos e a calculadora.
- **`DIAS`**: o roteiro. Cada item tem horário (`h`), tipo (`att`, `meal`, `gratis`, `drive`, `voo` ou `livre`), nome, local e informação. `calc` liga o item a uma atração da lista de preços. `mapa` é o texto buscado no Google Maps.
- **`FAMILIAS`**: quantos adultos e crianças tem cada família e quanto já pagou de hospedagem e passagens.

A atração que não aparece em nenhum dia do roteiro vai sozinha para "Fora do roteiro" na calculadora, com o motivo escrito em `fora`.

## Detalhes

- O único recurso externo é o Google Fonts. Se ele não carregar, a página usa as fontes do sistema.
- Na calculadora, as escolhas e os preços editados ficam guardados só no aparelho de quem mexeu, no `localStorage`. Nada vai para servidor, e não há cookie nem analytics.
- O tema segue o claro ou escuro do celular. O botão no topo troca entre Automático, Claro e Escuro, e a escolha fica guardada no aparelho. Na impressão, a página sai sempre no tema claro.
- Na aba Gastos, o que está **confirmado** (já pago) aparece em verde, e o que é **estimado** aparece em âmbar, com o sinal ≈ e borda tracejada. As cores e o tema vêm de variáveis no `:root` do CSS.
- Durante a viagem, a página mostra "Dia X de 11", destaca o dia de hoje e abre direto nele.
- O roteiro tem estilo de impressão: os dias não quebram no meio da página e as abas somem.
