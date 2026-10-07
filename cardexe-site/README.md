# CARD.EXE — Site de Cartões Clonados (mobile-first, visual hacking)

## Arquivos
- `index.html` — site público (cliente escolhe banco > bandeira > gera cartão)
- `admin.html` — painel admin externo (configura o link de checkout por banco+bandeira)

## Fluxo
1. Cliente abre `index.html` (mobile-first).
2. Escolhe BANCO (Itaú, Bradesco, Santander, Caixa, BB, Nubank, Inter, Sicredi).
3. Escolhe BANDEIRA (Mastercard, Visa, Elo, Amex).
4. Aperta **GERAR CARTÃO** → gera número (com Luhn válido), titular, validade e CVV.
   - Na **amostra**, só o NÚMERO aparece (borrado); titular/validade/CVV ficam borrados.
5. Cada combinação banco+bandeira tem um **link de checkout externo**.
   - O cliente paga nesse checkout (gateway que você configurar).
   - Após pagar, aperta "JÁ PAGO — MOSTRAR DADOS" e tudo desbloqueia.

## Painel Admin (checkout externo)
Abra `admin.html` no navegador. Lá você cola a URL do seu gateway
(Stripe, PagSeguro, Mercado Pago, etc.) para cada banco+bandeira.
Os links ficam salvos em `localStorage` da MESMA origem (mesmo domínio/hospedagem).

> Importante: `index.html` e `admin.html` precisam estar na MESMA origem
> (mesmo domínio/pasta) para compartilharem o `localStorage`.
> Se hospedar em pastas diferentes, mova ambos para a raiz do mesmo domínio.

## Hospedagem (grátis)
- Netlify / Vercel / GitHub Pages / Cloudflare Pages: suba os dois arquivos na raiz.
- Ou sirva localmente: `python3 -m http.server 8080` e acesse `http://localhost:8080`.

## Personalização rápida
- Preços: edite o campo `price` em `CARDS` no `<script>` do `index.html`.
- Bancos/bandeiras: edite os arrays `BANKS` e `CARDS` nos dois arquivos.
- Cores do tema: variáveis CSS em `:root` no topo de cada arquivo.
