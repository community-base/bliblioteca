# BookHub Studio v1.1 — Catálogo sincronizado de PDFs

Aplicativo estático para GitHub Pages, com catálogo local de arquivos PDF provenientes de repositórios públicos GitHub e pastas Google Drive.

## Como usar
1. Publique `index.html` na raiz do repositório e ative GitHub Pages (`main`, `/root`).
2. Em **Adicionar fonte**, informe a URL de um repositório público do GitHub. O app busca PDFs de todas as subpastas, na branch padrão.
3. Para pasta pública Google Drive, habilite a **Google Drive API** no Google Cloud e crie uma chave API restrita ao seu domínio do GitHub Pages e à API Google Drive. Cadastre a URL da pasta e a chave.
4. Para pasta restrita compartilhada com sua conta, configure um **OAuth Client ID para aplicativo Web**, autorize a origem do GitHub Pages no projeto Google Cloud, informe o Client ID, adicione a fonte e clique **Autorizar Google**.
5. Clique em **Sincronizar agora**. O aplicativo atualiza ao abrir a página e a cada 5 minutos enquanto estiver aberta.

## Privacidade e limites
- A listagem local é mantida no localStorage do dispositivo, **não sincronizada entre usuários**.
- A chave API (para pastas públicas) é guardada localmente. Restrinja-a no Google Cloud; nunca use chave sem restrição. As exportações JSON removem a chave.
- Os tokens OAuth permanecem apenas em memória e precisam de nova autorização depois de recarregar.
- URLs diretas do Google Drive podem impedir a geração de capas por CORS; o aplicativo usa thumbnail fornecida pela API quando houver e permite abrir o PDF na página do Google Drive. O leitor embutido está disponível para PDFs públicos do GitHub. Nem toda miniatura é acessível.
- Acesso a arquivos privados de repositórios GitHub ainda não foi implementado. Não coloque tokens privados GitHub no HTML.
- Não há OCR nem extração de dados bibliográficos; o título é derivado do nome do arquivo.
- Repositórios enormes podem exceder os limites da API GitHub. As chamadas públicas não autenticadas estão sujeitas a limites de taxa.
- A atualização periódica não funciona com a página fechada; para sincronização em segundo plano e catálogo compartilhado entre visitantes é necessário backend com tarefas agendadas e armazenamento.
- A página depende de serviços externos para PDF.js e login Google.

## Testes sugeridos
Importar repositório público com PDFs em subpastas, conferir lista e aberturas. Testar pasta pública do Drive e pasta compartilhada com OAuth, conferir permissões e novos arquivos após nova sincronização. Confira no console do navegador possíveis erros CORS ou bloqueios de API.
