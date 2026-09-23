# Relpps — automação do novo domínio

Domínio: https://relppscos.netlify.app

## Fluxo de pagamento

1. O checkout cria o Pedido de Venda no Bling.
2. A InfinitePay gera o checkout oficial para Pix/cartão.
3. O webhook da InfinitePay chega ao Netlify.
4. O backend confirma o pagamento novamente pela API `payment_check`.
5. O pedido é marcado como pago no Bling. O código usa `BLING_SITUACAO_PAGO_ID` se informado e, se estiver vazio, tenta descobrir automaticamente a situação “Pago” do módulo de Pedidos de Venda.
6. Para pedidos com Uber Moto, a entrega Uber Direct é criada automaticamente após a confirmação do pagamento. O ID e o tracking retornado pela Uber são gravados no pedido.

## Frete Correios via Melhor Envio

O checkout consulta a conta de produção do Melhor Envio e busca os serviços dos Correios disponíveis para a conta/rota. A interface apresenta PAC, SEDEX e Mini Envios quando a API devolver essas opções para o CEP e o pacote.

## Uber Moto via Uber Direct

A cotação é feita antes do pagamento. O token de cotação é assinado no backend e expira; o pedido não pode ser criado com uma cotação adulterada ou expirada. Após o pagamento aprovado, o backend usa o `quote_id` para criar a entrega real.

A Uber exige credenciais de produção, Customer ID, Client ID, Client Secret e aprovação/billing para entregas reais. Credenciais de sandbox servem somente para testes.

## Variáveis obrigatórias

- `PUBLIC_SITE_URL=https://relppscos.netlify.app`
- `CHECKOUT_TEST_MODE=false`
- `SHIPPING_TEST_MODE=false`
- `BLING_CREATE_ORDERS=true`
- `INFINITEPAY_HANDLE`
- `SUPABASE_URL` e `SUPABASE_SERVICE_ROLE_KEY`
- `BLING_CLIENT_ID`, `BLING_CLIENT_SECRET` e OAuth/refresh
- `MELHOR_ENVIO_CLIENT_ID`, `MELHOR_ENVIO_CLIENT_SECRET` e OAuth/refresh
- `UBER_DIRECT_CLIENT_ID`, `UBER_DIRECT_CLIENT_SECRET`, `UBER_DIRECT_CUSTOMER_ID`
- `SHIPPING_QUOTE_SECRET`, `RELPPS_ADMIN_RELEASE_SECRET`, `BLING_OAUTH_STATE_SECRET`

Nunca coloque os segredos externos no HTML, `config.js` ou Git.
