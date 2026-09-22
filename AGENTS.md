# AGENTS.md

Guia de trabalho para agentes e colaboradores do projeto paiparasempre_blog.

## Visão geral

Este repositório contém o site estático Jekyll do **Pai para sempre**, publicado em https://paiparasempre.com.br. O conteúdo é escrito em português do Brasil e inglês, com páginas, artigos, produtos afiliados e um tema baseado no Memoirs/Jekyll.

O stack principal é:

- Ruby 2.5.1 (definido em .ruby-version);
- Jekyll 4.0.1 e gems fixadas por Gemfile.lock;
- jekyll-multiple-languages-plugin 1.7.0 para as versões pt-BR e en;
- Liquid, Markdown via Kramdown, Sass e JavaScript sem bundler Node;
- Netlify CMS em admin/ e execução opcional via Docker.

## Estrutura do projeto

- _config.yml: configuração principal do Jekyll, plugins, idiomas, coleções, autores, paginação e integrações externas.
- _i18n/pt-BR/_posts/: artigos em português.
- _i18n/en/_posts/: versões em inglês dos artigos.
- _i18n/pt-BR.yml e _i18n/en.yml: textos da interface traduzidos.
- _pages/: páginas estáticas, normalmente com permalink e permalink_en.
- _produtos/: coleção produtos, com páginas de produtos e links afiliados.
- _layouts/: layouts Liquid (default, post, page, categorias, tags e autores).
- _includes/: componentes reutilizáveis de posts, navegação, comentários, anúncios e produtos.
- _sass/: fonte Sass do tema e do Bootstrap.
- assets/css/, assets/js/ e assets/images/: estilos, scripts e mídia servidos diretamente pelo site.
- admin/: configuração e entrada do Netlify CMS.
- site/_config.yml: configuração adicional usada pelo ambiente de site (host: 0.0.0.0).
- docker-compose.yml: definição legada para servir o Jekyll em localhost:4000.

## Ambiente e comandos

Use a versão de Ruby indicada em .ruby-version sempre que possível. Depois de instalar Ruby/Bundler compatíveis, instale as dependências com:

~~~sh
bundle install
~~~

Comandos usuais:

~~~sh
# Verificar se as gems do lockfile estão instaladas
bundle check

# Servir localmente com recarregamento
bundle exec jekyll serve --livereload

# Gerar o site em _site/
bundle exec jekyll build

# Diagnóstico nativo do Jekyll
bundle exec jekyll doctor
~~~

O servidor local normalmente fica em http://localhost:4000. _site/ é artefato gerado e está no .gitignore; não o adicione ao commit.

Para criar um artigo novo, o projeto já configura o jekyll-compose. Exemplo:

~~~sh
bundle exec jekyll compose "Título do artigo" --collection "i18n/pt-BR/_posts/"
~~~

Crie ou ajuste manualmente a versão correspondente em _i18n/en/_posts/ e mantenha as duas versões coerentes quanto ao tema, data e imagem.

Não há suíte de testes automatizados nem pipeline de lint identificada no repositório. Para mudanças em conteúdo, templates ou estilos, a verificação mínima é gerar o site com bundle exec jekyll build, revisar o diff e conferir as rotas afetadas no servidor local.

## Conteúdo e front matter

### Artigos

Use o padrão existente nos arquivos de _i18n/*/_posts/:

~~~yaml
---
layout: post
title: "Título"
comments: true
author: rk
date: 2023-01-03 10:00am
categories:
  - Categoria
image: assets/images/imagem.webp
imageshadow: true
---
~~~

- O nome do arquivo segue AAAA-MM-DD-slug.md.
- layout, author, date, categories e image devem seguir o padrão do artigo quando aplicável.
- tags é opcional, mas deve ser uma lista quando usado.
- Use caminhos de imagem relativos à raiz do site, como assets/images/image4.webp.
- Preserve o Markdown existente e evite inserir HTML quando Liquid/Markdown resolve o caso.

### Páginas

Para páginas localizadas, mantenha namespace, permalink e permalink_en coerentes. O layout usa chaves de tradução, por exemplo title: pages.contact e {% t contact.start_text %}. Quando uma nova chave de interface for criada, adicione-a aos dois arquivos _i18n/*.yml.

### Produtos

Produtos ficam em _produtos/*.md e usam a coleção produtos, geralmente com layout: page, link, plataforma, preco, image e comments: false. Revise cuidadosamente URLs afiliadas, preços e imagens antes de publicar.

## Internacionalização

Os idiomas configurados em _config.yml são pt-BR e en. O plugin de múltiplos idiomas gera as variantes a partir dos diretórios _i18n/; não mova artigos para um _posts/ raiz sem atualizar também a estratégia de localização.

Ao alterar a interface:

1. Prefira uma chave de tradução em _i18n/pt-BR.yml e _i18n/en.yml.
2. Use {% t chave %} nos templates em vez de duplicar texto fixo por idioma.
3. Verifique as rotas em português e inglês, especialmente /, /en/, /contato e /en/contact.
4. Lembre que index.html redireciona navegadores cujo idioma começa com en para /en/.

## Templates, estilos e scripts

- Alterações de marcação devem começar pelo layout ou include responsável, evitando duplicação entre páginas.
- assets/css/theme.scss é a entrada do tema; os parciais ficam em _sass/.
- Os scripts em assets/js/ são arquivos servidos diretamente. Não há package.json nem etapa de build Node.
- Faça mudanças pequenas em _layouts/ e _includes/, porque um erro Liquid pode quebrar várias páginas.
- Ao alterar imagens, mantenha nomes e extensões consistentes com os valores usados no front matter.
- Arquivos de terceiros como Bootstrap, Lunr e Prism já estão versionados em _sass/ e assets/js/; evite substituir esses arquivos sem necessidade clara.

## Integrações e dados sensíveis

_config.yml contém identificadores de serviços do site, como Analytics, Disqus, Formspree, reCAPTCHA e AdSense. Não introduza novas credenciais, tokens ou dados privados em commits, exemplos ou mensagens. Se uma integração precisar ser alterada, preserve a configuração existente e valide o site gerado sem expor valores sensíveis.

admin/config.yml usa Git Gateway, aponta para o domínio de produção e configura uploads em assets/images. Qualquer ajuste no CMS deve ser testado junto com o fluxo de criação de posts e produtos.

## Verificação antes de concluir uma mudança

- Rode bundle check; se faltar dependência, instale-a antes de tentar diagnosticar um erro do Jekyll.
- Rode bundle exec jekyll build e corrija erros Liquid, front matter ou de plugin.
- Para mudanças visuais, abra as páginas afetadas em localhost:4000 e confira desktop, idioma, imagens, links e paginação.
- Para mudanças em artigos traduzidos, confira as duas versões e suas imagens.
- Revise git diff e git status; não inclua _site/, caches ou arquivos temporários.

## Particularidades conhecidas

- No checkout atual não existe _posts/ na raiz; os 17 artigos de cada idioma vivem em _i18n/pt-BR/_posts/ e _i18n/en/_posts/.
- A configuração do Netlify CMS ainda declara a coleção de posts em _posts/. Se o CMS precisar ser usado para criar artigos, confirme e corrija esse alinhamento como uma tarefa própria antes de publicar.
- O docker-compose.yml está no formato legado, com jekyll na raiz. O docker compose config moderno pode rejeitá-lo por não haver a chave services; não presuma que docker compose up funcione sem adaptar o arquivo.
- O ambiente local pode não ter as gems instaladas. A ausência delas é um problema de preparação do ambiente, não necessariamente um erro do site.

## Estilo de colaboração

Mantenha o escopo de cada mudança pequeno, preserve o conteúdo existente e prefira corrigir a origem do problema no template/configuração em vez de criar exceções espalhadas. Não altere IDs de integração, links afiliados, textos traduzidos ou estrutura de URLs sem verificar o impacto nas duas versões do site.
