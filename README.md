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
- **Login obrigatório**, com duas contas (veja abaixo).

## Login e contas

O app pede e-mail e senha antes de mostrar qualquer dado (tela de login com a identidade Sellmed). Existem dois perfis, autenticados via Supabase Auth:

- **Edição** (`controletavi@sellmedbrasil.com`) — acesso completo: cria, edita, exclui procedimentos e anexa/remove reporte e nota fiscal.
- **Visualização** (`tavi@sellmedbrasil.com`) — só leitura: vê o dashboard e a base de procedimentos, abre e baixa os anexos já enviados, mas não vê o botão "Novo Procedimento" e o formulário de detalhes aparece bloqueado (sem campo editável, sem opção de anexar/remover arquivo).

As senhas foram definidas na criação das contas — troque-as quando quiser direto no painel do Supabase (Authentication → Users → selecionar o usuário → "Send password recovery" ou redefinir manualmente).

**Limite de segurança:** a restrição do perfil de visualização é aplicada tanto na tela quanto no banco de dados (Row Level Security do Supabase) — mesmo que alguém tente forçar uma inserção/edição pelas ferramentas do navegador com a conta de visualização, o Supabase recusa a operação (testado e confirmado).

O navegador permanece logado entre uma abertura e outra do arquivo (sessão salva localmente); use o botão **Sair** no canto superior direito para trocar de conta.

## Onde os dados ficam salvos

- Os dados dos procedimentos ficam numa tabela (`procedimentos`) no Supabase — banco na nuvem, projeto `sellmed-controle-tavi` (ref `rrpxgusloxqlrdxerpgi`).
- Os arquivos anexados (reporte e nota fiscal) ficam num bucket privado do Supabase Storage (`tavi-anexos`) — só acessível para quem estiver logado, via link temporário gerado na hora de abrir o anexo.
- Cada navegador também guarda uma cópia local (cache no `localStorage`) da última lista carregada, então se a internet cair o app continua mostrando os dados — mas não é possível criar/editar/excluir offline; volte a ter internet para salvar.
- O indicador no canto superior direito do cabeçalho mostra "Sincronizado", "Sincronizando…" ou "Sem conexão — mostrando cópia local".

**Importante sobre segurança:** o app usa a chave pública **anon** do Supabase (segura para expor num app cliente — quem pode fazer o quê é controlado por Row Level Security no banco, não pela chave). A senha do banco de dados (connection string `postgresql://...`) e a chave `service_role` usada para criar as contas **não estão em nenhum arquivo deste projeto** e não devem ser adicionadas aqui.

Hoje, como no app de Controle de Pagamentos, não há edição simultânea "ao vivo" entre duas pessoas — quem salvar por último sobrescreve os dados daquele campo.

## Identidade visual

- Logo oficial da Sellmed em destaque no cabeçalho (`assets/logo.svg`).
- Paleta: azul-marinho `#0C2F79`, teal `#1EA4A8` e verde `#73CC6E` (cores extraídas da logo/materiais institucionais da Sellmed), com a barra de destaque em degradê navy → teal → green.
- Tipografia Montserrat (títulos) e Inter (corpo de texto).
