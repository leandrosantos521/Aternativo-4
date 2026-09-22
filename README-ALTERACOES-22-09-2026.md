# Relpps — ajustes de catálogo e performance — 22/09/2026

## Alterações desta versão

- Removido o catálogo com filtros do meio da página inicial.
- A home agora prioriza Lançamentos e seleções de Colas, Cílios, Esmaltes, Sobrancelhas e Essenciais.
- O botão **VER TODOS OS PRODUTOS** abre a página de catálogo `#todos-produtos`.
- Filtros, busca, marcas, categorias e paginação ficam somente na página de todos os produtos.
- Adicionado botão para voltar ao início do site.
- Mantido o catálogo do Bling sem produtos fictícios em produção.
- Imagens do Bling passaram a carregar de forma progressiva, sem re-renderizar toda a grade a cada resposta da API.
- Primeiros produtos recebem prioridade; demais imagens carregam em segundo plano.
- Removido o `MutationObserver` global que ficava religando animações a cada alteração no DOM e podia deixar o scroll pesado.
- Removidas animações contínuas de repaint no fundo/cabeçalho para melhorar o desempenho ao rolar.
- Mantida a imagem original do Bling sempre que disponível, com proxy apenas como fallback.
- Página de produto, carrinho e checkout passaram a usar cabeçalho preto com a logo padrão da Relpps, mantendo a exceção do Club Relpps.
- Domínio oficial mantido como `https://relppscosmeticooo.netlify.app`.

## Testes feitos

- JavaScript validado com `node --check` em todos os arquivos `.js`.
- HTML verificado para IDs duplicados.
- IDs principais de catálogo (`productGrid`, `catalogPagination`, `emptyState`) ficaram únicos.
- Estrutura do catálogo dedicado e das cinco grades da home conferida.
