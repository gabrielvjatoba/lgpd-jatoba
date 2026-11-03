# lgpd-jatoba

Site oficial de transparência e LGPD do **Jatobá Lab** — projeto pessoal de Gabriel Jatobá — e modelo reutilizável para outros projetos.

- Produção (enquanto o DNS não propaga): <https://lgpd-jatoba.pages.dev>
- Domínio final: `lgpd.jatoba.tech` (anexado ao projeto, pendente de registro DNS na zona)
- Template: [`template/`](template/) · Página explicativa: [`public/modelo.html`](public/modelo.html)

## O que é

Um site **estático puro**: HTML + CSS, sem React, sem build, sem bundler, sem backend, sem banco, sem JavaScript próprio, sem fontes externas, sem analytics e sem cookies de rastreamento.

Conteúdo essencial e verificável sobre privacidade, termos de uso e governança de LGPD — não uma peça de marketing.

## Estrutura

```
public/
  index.html                 # home: o que é o lab, controlador, DPO, status
  privacidade.html           # política completa (dados, bases, IA, retenção, direitos)
  termos.html                # termos de uso
  lgpd.html                  # governança: ROPA resumido, RIPD, DSAR, incidentes
  modelo.html                # explica o uso do repo como template
  styles.css                 # CSS único (modo escuro automático, estilos de impressão)
  404.html                   # página de erro
  robots.txt                 # indexação + sitemap
  sitemap.xml                # 5 URLs públicas
  _headers                   # CSP, HSTS, nosniff, frame-options, permissions-policy
  .well-known/security.txt   # canal de relato de vulnerabilidades
template/
  index.html                 # starter de uma página com placeholders
  README.md                  # checklist de adaptação
README.md
LICENSE
```

## Rodar localmente

Não há build. Basta servir a pasta `public/`:

```bash
cd public
python3 -m http.server 8080
# abra http://localhost:8080
```

Abrir `index.html` direto no navegador também funciona, mas links absolutos (`/styles.css`) exigem um servidor local.

## Editar

1. **Textos jurídicos** — `public/privacidade.html`, `public/termos.html`, `public/lgpd.html`. Mantenha a versão e a data no topo sincronizadas nas três páginas e no rodapé.
2. **Dados do controlador** — aparece na home (`dl.deflist`), na privacidade (seção 2) e no rodapé de todas as páginas.
3. **Fornecedores** — atualize em dois lugares: `public/privacidade.html` (seção 8) e `public/lgpd.html` (seção 7). As tabelas precisam contar a mesma história.
4. **Retenção** — `public/privacidade.html` (seção 10) e `public/lgpd.html` (ROPA).
5. **Estilo** — `public/styles.css`. Tudo usa variáveis CSS no `:root`; o modo escuro é automático via `prefers-color-scheme`.
6. **Cabeçalhos** — `public/_headers`. Se adicionar JS ou estilo inline, a CSP atual (`script-src 'none'`, `style-src 'self'`) vai bloquear. Ajuste com consciência.
7. **Domínio** — `robots.txt`, `sitemap.xml`, `security.txt` e a tag `canonical` das páginas.

## Publicar no Cloudflare Pages

```bash
CLOUDFLARE_API_TOKEN=... \
CLOUDFLARE_ACCOUNT_ID=90bbb32fea53c037d5add227b9ff3458 \
npx wrangler@latest pages deploy public --project-name=lgpd-jatoba --branch=main
```

Não há comando de build. O diretório de saída é `public/`.

### Domínio customizado `lgpd.jatoba.tech`

O projeto foi publicado em `lgpd-jatoba.pages.dev`. O domínio `lgpd.jatoba.tech` **já está anexado ao projeto Pages**, mas ficou com status `pending` porque a zona `jatoba.tech` está em outra conta Cloudflare e o token atual não enxerga essa zona (`GET /zones?name=jatoba.tech` retorna lista vazia). Falta apenas criar o registro DNS na conta que detém a zona:

1. Entre na conta Cloudflare que possui a zona `jatoba.tech`.
2. Vá em **DNS → Records → Add record**.
3. Crie um `CNAME`:
   - Nome: `lgpd`
   - Destino: `lgpd-jatoba.pages.dev`
   - Proxy: ativado (nuvem laranja)
4. Volte em **Workers & Pages → lgpd-jatoba → Custom domains** e confirme que `lgpd.jatoba.tech` aparece como ativo (a validação do certificado costuma levar alguns minutos).

Se preferir refazer o vínculo pelo dashboard: **Workers & Pages → lgpd-jatoba → Custom domains → Set up a custom domain** → `lgpd.jatoba.tech`.

Alternativa por API, com um token que tenha `Zone:DNS:Edit` e `Zone:Zone:Read` na zona `jatoba.tech`:

```bash
curl -X POST "https://api.cloudflare.com/client/v4/accounts/90bbb32fea53c037d5add227b9ff3458/pages/projects/lgpd-jatoba/domains" \
  -H "Authorization: Bearer $CF_TOKEN" \
  -H "Content-Type: application/json" \
  --data '{"name":"lgpd.jatoba.tech"}'
```

## Usar como template

O repositório está marcado como template no GitHub. Duas opções:

- **Página única:** copie `template/index.html` e siga `template/README.md`.
- **Conjunto completo:** copie `public/` e substitua controlador, DPO, fornecedores, prazos e domínio.

Checklist resumido (o completo está em `template/README.md`):

- [ ] Substituir todos os marcadores `[...]`.
- [ ] Ajustar bases legais ao que o produto realmente faz.
- [ ] Ajustar prazos de retenção para algo executável.
- [ ] Listar todos os fornecedores e países.
- [ ] Remover seções que não se aplicam (ex.: IA).
- [ ] Revisar com apoio jurídico.
- [ ] Atualizar `robots.txt`, `sitemap.xml`, `security.txt` e `canonical`.
- [ ] Testar em produção.

## Decisões e placeholders

Itens que dependem de decisão do Gabriel e estão registrados de forma explícita no site:

| Item | Situação | Onde |
|---|---|---|
| CNPJ / pessoa jurídica | Projeto é pessoa física; CNPJ não existe | Home, privacidade §2 |
| `lgpd@jatoba.tech` | Ainda não existe; canal é `gabrielvjatoba@gmail.com` | Todas as páginas |
| DPA com suboperadores | Termos padrão avaliados; contratos específicos pendentes | LGPD §7 e §9 |
| Modelo de RIPD | Em elaboração; nenhum RIPD exigível nesta versão | LGPD §4 |
| Provedor de e-mail | Não detalhado nominalmente | Privacidade §8 |
| Foro | Regra do domicílio do consumidor + comarca do controlador em Alagoas | Termos §16 |

Para trocar o e-mail oficial quando `lgpd@jatoba.tech` existir:

```bash
grep -rl "gabrielvjatoba@gmail.com" public template README.md
# substitua nos arquivos listados e atualize security.txt
```

## Obrigatório vs. boa prática

O site separa explicitamente os dois na página `public/lgpd.html` (§2). Resumo:

**Obrigatório pela LGPD:** indicação de encarregado e canal (art. 41), registro de operações (art. 37), informação clara (arts. 9º e 18), resposta a titulares em 15 dias (art. 19), comunicação de incidente relevante (art. 48), base legal para transferência internacional (art. 33), RIPD quando exigido (art. 38).

**Boa prática adotada:** política publicada, resumo público do ROPA, CSP e cabeçalhos de segurança, `security.txt`, ausência de cookies de rastreamento, ZDR no gateway de IA, registro de incidentes e plano de maturidade.

## Segurança

- CSP sem `unsafe-inline`, `script-src 'none'`.
- `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Referrer-Policy`, `Permissions-Policy`, HSTS.
- Sem segredos no repositório. Chaves ficam fora do versionamento.
- Relatos de vulnerabilidade: veja `public/.well-known/security.txt`.

## Licença

MIT — veja [`LICENSE`](LICENSE). A marca “Jatobá Lab” e a identidade visual não são licenciadas para sugerir endosso.

## Aviso

Este site é informativo e **não constitui parecer jurídico**. Não há certificação de LGPD, ISO 27001 ou equivalente. Os textos descrevem práticas e intenções do projeto na versão 1.0 (3 de novembro de 2026).
