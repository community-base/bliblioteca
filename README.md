# BookHub Studio v1.0 — Biblioteca Mista

Biblioteca virtual em HTML estático, com layout dark, capas geradas a partir da primeira página de PDFs e leitura integrada no navegador.

## Início rápido

1. Abra `index.html` no navegador moderno (Chrome/Edge/Firefox) com acesso à internet.
2. Use **+ PDF privado** para adicionar PDFs do seu computador. Eles ficam apenas na sessão atual: **não são enviados nem salvos**.
3. Use **Adicionar link** para cadastrar um PDF acessível publicamente, incluindo links de PDFs compartilhados do Google Drive.
4. Use **Importar GitHub** para buscar arquivos `.pdf` em repositórios **públicos**. Informe usuário, repositório e branch.
5. Abra um cartão por **Ler PDF**, pesquise ou filtre pelas estantes.
6. **Exportar catálogo** salva um JSON com os registros **públicos** cadastrados, e **Importar catálogo** restaura esses registros em outro navegador.

## GitHub Pages

Crie um repositório, envie `index.html` na **raiz** (em letras minúsculas), ative **Settings > Pages > Deploy from a branch > main > /(root)**. O site ficará em `https://USUARIO.github.io/REPOSITORIO/` quando o Pages publicar.

## O que é público ou privado aqui?

- **Público:** PDFs abertos por URL ou importados do GitHub. Os links e seus metadados ficam salvos no `localStorage` do navegador; o JSON exportado contém apenas estes registros. **O catálogo não é sincronizado automaticamente para outros visitantes**.
- **Privado local:** PDFs selecionados do próprio computador. O arquivo permanece no navegador por meio de um `blob:` URL temporário, somente enquanto a página está aberta. Não é publicado nem sincronizado; desaparece do catálogo quando a página é recarregada.
- **Privado na nuvem:** *não implementado nesta versão*. Acesso a Google Drive privado exige autenticação OAuth, autorização do usuário, controle de sessão e uso da API Google Drive. Não coloque tokens, credenciais ou links secretos no HTML ou no repositório público.

## Capas e Google Drive

A geração de capas usa a biblioteca PDF.js 4.10.38 pelo CDN `cdnjs.cloudflare.com`. Requer internet. PDFs remotos também precisam permitir acesso do navegador via CORS; sem essa autorização, a capa poderá aparecer como um símbolo de livro. O leitor integrado pode igualmente ser bloqueado pelas políticas do servidor de origem (por exemplo, restrições a `iframe`). Use o botão **Nova guia** para abrir externamente.

O Google Drive pode oferecer links de visualização, não um download direto com CORS. Nessas condições, o BookHub **não consegue garantir uma miniatura extraída do PDF**. Esta é uma limitação de acesso, não de formato. PDFs privados no Drive não são listados automaticamente.

## Limitações da versão

- Nenhum backend, login ou armazenamento de PDF online.
- Repositórios GitHub privados não são importados.
- No máximo 100 PDFs por importação GitHub; a API pode limitar consultas e truncar árvores grandes.
- Somente registros públicos são persistidos localmente, não compartilhados entre usuários.
- A extração de capa e a incorporação de PDFs externos dependem do servidor que hospeda o PDF.
- A leitura de um livro público no leitor depende de sua URL continuar disponível.

## Testes

Sintaxe JavaScript verificada com `node --check`. Publicação em ambiente real, acesso a PDFs de terceiros e interface ainda exigem teste no navegador.
