# Template,  página de privacidade e transparência

Starter de **uma página** em HTML e CSS puros, sem build, sem dependências e sem rastreamento. Serve para publicar rapidamente uma política de privacidade legível e um resumo de governança.

> **Modelo,  adapte e revise antes de publicar.** O texto é um ponto de partida, não um parecer jurídico e não garante conformidade com a LGPD.

## Como usar

1. Copie `index.html` para o seu projeto.
2. Substitua todos os marcadores entre colchetes (lista abaixo).
3. Apague as seções que não se aplicam,  texto genérico que não corresponde à realidade é pior do que ausência de texto.
4. Revise com apoio jurídico antes de uso comercial.
5. Publique em qualquer host estático (Cloudflare Pages, GitHub Pages, Netlify, S3).

O arquivo é autocontido: o CSS está em um bloco `<style>`. As fontes Geist são carregadas de `../public/fonts/` por caminho relativo (para pré-visualizar dentro do repositório). Ao copiar o template para outro projeto, leve a pasta `fonts/` junto e ajuste os caminhos,  ou remova os `@font-face` para usar a fonte do sistema. Se você for publicar com a CSP restritiva do conjunto completo (`public/_headers`, que usa `style-src 'self'`), mova o bloco para um arquivo `styles.css` e troque por `<link rel="stylesheet" href="/styles.css">`.

## Marcadores

| Marcador | O que colocar |
|---|---|
| `[CONTROLADOR]` | Razão social ou nome completo do controlador |
| `[CNPJ]` | CNPJ ou “pessoa física, sem CNPJ” |
| `[DPO]` | Nome do encarregado de dados |
| `[EMAIL]` | E-mail de privacidade monitorado (ex.: `lgpd@seudominio.com`) |
| `[ENDEREÇO]` | Endereço completo ou, no mínimo, cidade/UF e país |
| `[PROVEDOR 1..3]` | Hospedagem, CDN, e-mail, gateway de IA etc. |
| `[PAÍS]` / `[PAÍSES]` | Onde cada fornecedor trata os dados |
| `[PRAZO]` | Prazo real de retenção por categoria |
| `[VERSÃO]` | Versão do documento (ex.: `1.0`) |
| `[DATA]` | Data da última atualização (ex.: `3 de novembro de 2026`) |
| `[DOMÍNIO]` | Domínio canônico, sem `https://` |
| `[CATEGORIA]`, `[EXEMPLOS]`, `[ORIGEM]`, `[FINALIDADE]` | Linhas adicionais do inventário de dados |
| `[DESCREVA OS COOKIES REAIS]` | Texto sobre cookies, ou a declaração de que não há |

## Checklist antes de publicar

### Conteúdo

- [ ] Todos os marcadores `[...]` foram substituídos.
- [ ] Controlador e DPO existem e o canal é monitorado.
- [ ] Cada finalidade tem base legal compatível com o art. 7º da LGPD.
- [ ] Dados sensíveis (art. 11) foram removidos do escopo ou têm base específica.
- [ ] Prazos de retenção são reais e executáveis.
- [ ] Todos os fornecedores que veem dados estão listados.
- [ ] A seção de transferência internacional reflete os países reais.
- [ ] Se há IA: prompts, memória, logs, retenção e provedores estão descritos.
- [ ] Se não há IA: a seção foi removida.
- [ ] Cookies descritos correspondem ao que o site realmente define.
- [ ] Foro e limitação de responsabilidade estão adequados ao seu caso.
- [ ] Alguém com conhecimento jurídico revisou.

### Técnico

- [ ] O site abre sem JavaScript.
- [ ] Os links de e-mail e âncoras funcionam.
- [ ] A página é navegável por teclado (Tab) e tem contraste adequado.
- [ ] O layout funciona em telas de 320 px a 1440 px.
- [ ] `lang="pt-BR"` está correto (ajuste se o idioma mudar).
- [ ] `title` e `meta description` foram personalizados.
- [ ] `canonical` aponta para o domínio certo.
- [ ] As fontes Geist foram copiadas (`fonts/`) e os caminhos dos `@font-face` conferem.
- [ ] Se publicar com CSP: `style-src` permite o CSS e `script-src 'none'` não quebra nada.

### Publicação

- [ ] `robots.txt` e `sitemap.xml` apontam para o domínio correto.
- [ ] `security.txt` tem e-mail válido e `Expires` no futuro.
- [ ] HTTPS está ativo.
- [ ] A página foi testada em produção, não só localmente.

## O que este template não faz

- Não cria base legal, contrato ou DPA.
- Não substitui RIPD, ROPA ou avaliação de fornecedores.
- Não implementa consentimento, gestão de cookies ou DSAR.
- Não garante conformidade com LGPD, GDPR ou qualquer outra norma.

## Licença

MIT. Veja o `LICENSE` do repositório.
