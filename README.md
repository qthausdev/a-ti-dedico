# A ti, dedico 💜

Página pessoal com um campo de lírios em pixel art, céu estrelado animado, foto do casal, playlist com prévias do Spotify e um caderninho de mensagens.

## Recursos

- Layout responsivo e animação que respeita a preferência por movimento reduzido.
- Pétala, de Djavan, permanece na primeira posição da playlist.
- Adição de músicas por link do Spotify, sem sair da página.
- Cartinhas com texto, quebras de linha e emojis.
- Persistência das músicas e cartinhas em banco de dados.

## Estrutura

- `public/`: HTML, CSS, JavaScript e imagens.
- `worker/index.js`: API e entrega dos arquivos em Cloudflare Workers.
- `db/schema.ts`: esquema do banco SQLite/D1.
- `drizzle/`: migrações versionadas; não reescrever as que já foram aplicadas.
- `scripts/build.mjs`: gera o Worker em `dist/server/index.js`.

## Instalação e build

Requer Node.js e npm.

```sh
npm ci
npm run build
```

O build atual gera um Cloudflare Worker. O banco precisa ser conectado ao binding `DB`, com as migrações de `drizzle/` aplicadas.

## Publicação na Vercel

Este repositório contém o código completo da versão atual, mas o backend usa Cloudflare Workers e D1. Importá-lo na Vercel, sem adaptação, não preserva as funções de salvar músicas e cartinhas.

Para migrar:

1. Servir o conteúdo de `public/` como arquivos estáticos.
2. Adaptar as rotas `GET/POST /api/songs` e `GET/POST /api/notes` de `worker/index.js` para Vercel Functions.
3. Conectar um banco persistente compatível com a Vercel e adaptar o acesso ao binding `DB`.
4. Aplicar o esquema e transferir os registros atuais antes de trocar o endereço usado pelas pessoas.
5. Configurar acesso privado/autenticação antes de disponibilizar a página: a proteção da hospedagem anterior não faz parte deste código.

Os registros salvos (músicas e cartinhas) ficam no banco da hospedagem atual e não são incluídos neste repositório. A música Pétala é fixada pelo código.

## Observações

A lista de músicas da página é independente de playlists da conta Spotify. A disponibilidade e reprodução das prévias dependem do Spotify. Não há credenciais do Spotify no projeto.

As imagens são pessoais. Mantenha o repositório privado.
