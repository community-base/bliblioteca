# BookHub Studio v1.3 — Seleção de fontes e sincronização

Aplicação HTML estática, publicada no GitHub Pages.

## Novo fluxo

1. Abra **Adicionar fontes**.
2. Para GitHub, informe o nome de usuário em **Usuário ou organização GitHub** e clique **Pesquisar fontes**. Marque repositórios. Ou cole a URL de um repositório e clique **Explorar pastas** para escolher subpastas.
3. Para Google Drive, cole a URL de uma pasta e configure a chave Google API (pasta pública acessível via API) ou OAuth Client ID (pasta compartilhada/privada com acesso autorizado). Clique **Explorar pastas** e marque as pastas desejadas.
4. Clique **Salvar seleção e sincronizar**. O aplicativo salva as fontes no armazenamento local, procura PDFs, fecha a área de configuração e volta ao catálogo.
5. **Sincronizar agora** atualiza todas as fontes; atualizações automáticas são realizadas a cada 5 minutos enquanto a aba estiver ativa.

## Limites e segurança

- A configuração do catálogo fica no navegador e não é compartilhada entre dispositivos.
- GitHub: somente repositórios públicos. A API anônima tem limites de requisição.
- Drive: a API não permite enumerar uma pasta privada somente com o URL; é necessário configurar credenciais Google Cloud e autorização OAuth para arquivos restritos. Arquivos compartilhados por link também podem exigir autenticação.
- O Google Drive é percorrido recursivamente nas pastas selecionadas, com limite de 250 pastas por fonte.
- Cada origem é atualizada no catálogo após sincronização bem-sucedida; falhas preservam resultados anteriores.
- A miniatura da primeira página usa PDF.js para PDFs públicos do GitHub. No Drive, utiliza a miniatura oferecida pelo serviço quando disponível.
- O HTML não autentica nem sincroniza com o navegador fechado. Não publique arquivos privados no repositório público.
- Em uso coletivo, é recomendado um backend autenticado para compartilhar o catálogo e proteger tokens.

## Publicação

Envie `index.html`, `README.md` e `.nojekyll` à raiz da branch `main`; em Settings → Pages, selecione Deploy from a branch → main → /(root). O nome deve ser `index.html` em minúsculas.
