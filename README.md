# BookHub Studio v1.2

Biblioteca virtual em HTML estático, com catálogo de PDFs em repositórios públicos GitHub e pastas Google Drive acessíveis por API. Visual escuro, busca, miniaturas e leitor de PDFs quando suportado pelo navegador e pela origem.

## Publicar no GitHub Pages

1. Abra o repositório **community-base/bliblioteca** (a grafia é `bliblioteca`).
2. Na branch `main`, substitua o arquivo **`index.html`** da raiz pelo arquivo `index.html` deste pacote. O nome deve ser totalmente minúsculo.
3. Adicione `README.md` e `.nojekyll` na mesma pasta raiz.
4. Em **Settings > Pages**, escolha **Deploy from a branch**, branch **main**, pasta **/(root)**. Verifique o resultado em **Actions**.
5. Abra `https://community-base.github.io/bliblioteca/` e atualize com Ctrl+Shift+R caso o navegador mostre uma versão antiga.

## Usar com GitHub

Clique em **Adicionar fonte** > **Repositório público do GitHub**. Cole a URL completa, por exemplo `https://github.com/community-base/bliblioteca`, informe o nome da coleção e escolha **Adicionar e sincronizar**. O aplicativo consulta a API pública GitHub, percorre a árvore de arquivos da branch padrão e reconhece caminhos terminados em `.pdf`. Se houver arquivos novos ou removidos, o catálogo daquela fonte é atualizado. Repositórios privados e árvores muito grandes não são suportados nesta versão.

## Usar com Google Drive

Não basta colar um link de pasta para consultar sua lista de PDFs. É necessário habilitar a **Google Drive API** em um projeto Google Cloud.

- **Pasta pública:** cadastre a URL da pasta e uma chave API restrita à Google Drive API e à origem do seu site. O serviço pode recusar a listagem de determinados compartilhamentos sem OAuth; nesse caso use autenticação.
- **Pasta compartilhada ou privada:** configure um *OAuth Client ID* do tipo **Web application**, incluindo `https://community-base.github.io` nas origens JavaScript autorizadas. Selecione **Pasta compartilhada comigo (OAuth)**, informe o Client ID e clique em **Autorizar Google**. A conta que autoriza deve ter permissão para listar os arquivos.

**Segurança:** nunca coloque *client secret*, senha ou token pessoal GitHub no HTML. Uma chave de API frontend não é segredo e precisa de restrições no Google Cloud. Tokens OAuth são mantidos somente na sessão JavaScript; fontes e chaves API são salvas em `localStorage` do navegador, portanto utilize apenas chaves públicas restritas. Para acesso de vários usuários com catálogo privado compartilhado, será necessário um backend com regras de acesso.

## Funcionalidades e limites

- Atualiza as fontes ao abrir e a cada cinco minutos enquanto a aba permanecer ativa; não sincroniza com o navegador fechado.
- Salva fontes e metadados no armazenamento local daquele navegador. Não publica um catálogo global compartilhado.
- PDF.js é carregado de CDN para miniaturas da primeira página dos arquivos GitHub; ausência de rede, bloqueio de CDN ou CORS podem impedir a capa. Nesse caso o cartão com título continua disponível.
- Miniaturas do Google Drive dependem da disponibilidade do `thumbnailLink` e das permissões de leitura. PDFs do Drive abrem no serviço de origem.
- Os arquivos privados não são copiados para o GitHub Pages.
- Para testar offline, o arquivo pode abrir localmente, mas a sincronização exige rede e o OAuth Google exige uma origem HTTPS autorizada.

## Diagnóstico

- **404:** verifique a grafia `bliblioteca`, nome `index.html`, a branch `main` e o status em **Actions**.
- **Catálogo vazio:** confirme a existência de PDFs na fonte, permissões de leitura e eventual erro exibido abaixo dos filtros.
- **Google 403:** verifique se a API foi habilitada, permissões da pasta, chave restrita e OAuth.
- **Capa ausente:** pode ser um bloqueio de CORS, biblioteca PDF.js indisponível ou documento restrito.

## Estrutura

```text
index.html
README.md
.nojekyll
```

A aplicação é estática. O arquivo `index.html` foi revisado estruturalmente; a autenticação e cada fonte precisam ser validadas no navegador com permissões reais.
