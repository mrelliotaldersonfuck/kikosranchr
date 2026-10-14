# Kiko’s Ranch · Painel de Cotações

Tela de cotações de commodities do agro, pronta para a Vercel.

## Estrutura
- `index.html` — a tela (cores da marca no topo do `<style>`, bloco `:root`)
- `logo.svg` — logo provisória; **substitua pelo arquivo oficial com o mesmo nome** (ou troque `logo.svg` por `logo.png` no `index.html`)
- `api/cotacoes.js` — função da Vercel que busca os preços e converte para R$

## Publicar
1. Crie um repositório no GitHub e suba estes arquivos.
2. Na Vercel: **Add New → Project → Import** o repositório. Framework: *Other*. Sem build.
3. Deploy. A tela fica em `https://seu-projeto.vercel.app`.

Ou pela linha de comando: `npx vercel --prod` dentro desta pasta.

## Na TV
O painel detecta Smart TVs (Samsung Tizen, LG webOS etc.) e entra sozinho no **modo TV**, com letras maiores e gráficos menores. `?tv=1` força o modo TV em qualquer tela; `?tv=0` desliga. `?debug=1` mostra no canto o tamanho de tela que o navegador informa e a escala aplicada.

## Opções na URL
- `?tv=1` — modo TV (letras maiores para ver de longe)
- `?destaque=soja` — muda o card de destaque (`boi`, `bezerro`, `acucar`, `milho`, `soja`)

Ordem dos cards: lista `ORDEM` em `api/cotacoes.js`. Logo: troque `logo.svg` (aparece ao lado do nome).

## Fontes
- **Boi gordo (SP e por estado):** Indicador do Boi Datagro.
- **Bezerro:** Datagro, reposição Nelore macho, São Paulo (R$/kg).
- **Açúcar VHP:** bolsa de Nova York, contrato nº 11, ao vivo durante o pregão pelo Yahoo Finance (~15 min de atraso), mostrado em R$/saca de 50 kg (convertido pelo dólar do momento), com o valor original em centavos de US$/libra-peso embaixo. Reserva: fechamento publicado pela Notícias Agrícolas.
- **Milho (Campinas), soja (Paraná):** indicadores diários CEPEA/ESALQ.
- **Etanol hidratado, hidratado outros fins e anidro:** indicadores semanais CEPEA/ESALQ.
- Todos lidos das páginas públicas da Notícias Agrícolas, que republica esses indicadores. Cada card mostra a data da última atualização.
- **Câmbio:** Investing.com, com reserva no Yahoo Finance.
- **Ibovespa, Nasdaq e S&P 500:** Yahoo Finance.
- **CDI e Selic:** API oficial do Banco Central.
- A tela se atualiza sozinha a cada 15 min, sem recarregar (as fontes publicam 1x por dia, ou 1x por semana no etanol; dólar e bolsas mudam ao longo do dia). Quando você publica uma versão nova no Vercel, as telas abertas se recarregam sozinhas.

**Futuros B3 (card rotativo, 8 s cada):** boi gordo, milho, soja (convertida para R$ pelo dólar do dia) e etanol hidratado (em R$/litro).

Para trocar praça ou produto, edite a lista `CEPEA` em `api/cotacoes.js`.
