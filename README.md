# Controle TAVI — Sellmed Brasil

App estático (um único `index.html`, sem servidor, sem build) para controle dos procedimentos TAVI (Venus A Pro), na identidade visual da Sellmed. O app em si **não está publicado em lugar nenhum** — continua sendo só um arquivo local, aberto direto no navegador. Os dados e anexos, porém, ficam sincronizados na nuvem via Supabase, então qualquer pessoa que abrir este mesmo arquivo (em qualquer computador) vê a mesma base, atualizada.

## Como abrir

Dê duplo clique em `index.html` (abre no navegador padrão) ou arraste o arquivo para o Chrome/Firefox. Precisa de internet para carregar e salvar os dados.

## O que o app faz

- Reproduz a planilha original (Dashboard + Base de Procedimentos), já importada com os 56 casos existentes.
- Dashboard 100% automático: os cards de status, a matriz por região e o gráfico de barras são recalculados a cada inclusão, edição ou exclusão — não precisa atualizar nada manualmente.
- **Novo Procedimento**: botão no topo abre um formulário com todos os campos da planilha (paciente, cidade, UF — a região é preenchida automaticamente a partir da UF —, hospital, médico, data, status, prótese, responsável, crimper/especialista).
- **Editar/excluir**: clique em qualquer linha da tabela para abrir o mesmo formulário já preenchido, alterar dados ou excluir o caso.
- **Anexos**: cada paciente (tanto ao criar um novo procedimento quanto ao editar um já existente) tem 2 campos de anexo — **Reporte** e **Nota Fiscal**. Os ícones "R" e "NF" na tabela mostram rapidamente quais pacientes já têm cada anexo.
- Busca por paciente/cidade/hospital/médico e filtros por status e região.

## Onde os dados ficam salvos

- Os dados dos procedimentos ficam numa tabela (`procedimentos`) no Supabase — banco na nuvem, projeto `sellmed-controle-tavi` (ref `rrpxgusloxqlrdxerpgi`).
- Os arquivos anexados (reporte e nota fiscal) ficam num bucket do Supabase Storage (`tavi-anexos`).
- Cada navegador também guarda uma cópia local (cache no `localStorage`) da última lista carregada, então se a internet cair o app continua mostrando os dados — mas não é possível criar/editar/excluir offline; volte a ter internet para salvar.
- O indicador no canto superior direito do cabeçalho mostra "Sincronizado", "Sincronizando…" ou "Sem conexão — mostrando cópia local".
- Não há login: qualquer pessoa com o arquivo `index.html` (e internet) lê e edita os dados. Para uso interno da equipe isso é aceitável, mas evite compartilhar o arquivo fora da empresa.

**Importante sobre segurança:** o app usa a chave pública **anon** do Supabase (segura para expor num app cliente — o acesso é controlado por Row Level Security no banco). A senha do banco de dados (connection string `postgresql://...`) **não está em nenhum arquivo deste projeto** e não deve ser adicionada aqui.

Se no futuro quiser adicionar login (usuário/senha) ou sincronização em tempo real entre pessoas editando ao mesmo tempo, dá para evoluir isso — hoje, como no app de Controle de Pagamentos, quem salvar por último sobrescreve os dados daquele campo (sem edição simultânea "ao vivo").

## Identidade visual

- Logo oficial da Sellmed em destaque no cabeçalho (`assets/logo.svg`).
- Paleta: azul-marinho `#0C2F79`, teal `#1EA4A8` e verde `#73CC6E` (cores extraídas da logo/materiais institucionais da Sellmed), com a barra de destaque em degradê navy → teal → green.
- Tipografia Montserrat (títulos) e Inter (corpo de texto).
