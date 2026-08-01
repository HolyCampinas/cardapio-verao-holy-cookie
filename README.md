# Cardápio de Verão — Holy Cookie

Página de coleta e votação de sugestões de produtos para o cardápio de verão.

**No ar:** https://holycampinas.github.io/cardapio-verao-holy-cookie/

## Como funciona

1. O colaborador cola o link de um reel do Instagram — a capa do vídeo é puxada e salva automaticamente.
2. Se a capa não mostra bem o produto pronto, ele sobe uma foto (a foto manual sempre ganha da capa automática).
3. Todo mundo vê a galeria e vota nos produtos que quer ver na loja.
4. A aba **Selecionados** ordena tudo por número de votos — é dela que sai o cardápio final.

## Infra

Projeto Supabase isolado (`wjirwqgiuqjxxoriqddj`, org Holy Cook Campinas) — **não compartilha nada com o Sistema Holy Cook**.

- Tabelas `sugestoes` e `votos`, ambas com RLS. Ninguém consegue apagar uma sugestão pela página.
- Bucket público `fotos` (capas automáticas em `capas/`, uploads em `envios/`).
- Edge function `capa`: recebe o link, consulta o oEmbed do Instagram, baixa a capa e republica no Storage — a URL original do fbcdn é assinada e expira.

A chave `anon` no HTML é pública por design; o que protege os dados são as políticas de RLS.
