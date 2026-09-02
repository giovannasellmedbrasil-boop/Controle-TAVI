# Controle TAVI — Sellmed Brasil

App estático (um único `index.html`, sem servidor, sem build) para controle dos procedimentos TAVI (Venus A Pro), na identidade visual da Sellmed. Este projeto **não está publicado em lugar nenhum** — é só para uso local, no seu computador.

## Como abrir

Dê duplo clique em `index.html` (abre no navegador padrão) ou arraste o arquivo para o Chrome/Firefox.

## O que o app faz

- Reproduz a planilha original (Dashboard + Base de Procedimentos), já importada com os 56 casos existentes.
- Dashboard 100% automático: os cards de status, a matriz por região e o gráfico de barras são recalculados a cada inclusão, edição ou exclusão — não precisa atualizar nada manualmente.
- **Novo Procedimento**: botão no topo abre um formulário com todos os campos da planilha (paciente, cidade, UF — a região é preenchida automaticamente a partir da UF —, hospital, médico, data, status, prótese, responsável, crimper/especialista).
- **Editar/excluir**: clique em qualquer linha da tabela para abrir o mesmo formulário já preenchido, alterar dados ou excluir o caso.
- **Anexos**: cada paciente (tanto ao criar um novo procedimento quanto ao editar um já existente) tem 2 campos de anexo — **Reporte** e **Nota Fiscal**. Os ícones "R" e "NF" na tabela mostram rapidamente quais pacientes já têm cada anexo.
- Busca por paciente/cidade/hospital/médico e filtros por status e região.

## Onde os dados ficam salvos

Tudo é gravado **no navegador deste computador**:

- Os dados dos procedimentos ficam no `localStorage`.
- Os arquivos anexados (reporte e nota fiscal) ficam no `IndexedDB` do navegador, para suportar PDFs/imagens sem esbarrar no limite pequeno do `localStorage`.

Isso significa:

- Não há sincronização entre aparelhos — se abrir em outro computador ou em outro navegador, os dados não aparecem lá (é uma cópia nova, com a base original de 56 casos).
- Se limpar o cache/dados de navegação do navegador, os procedimentos e anexos incluídos são perdidos. Evite usar o modo anônimo/privado para uso contínuo.
- Recomendado: sempre usar o mesmo navegador (Chrome ou Firefox, de preferência) como "principal" para este app.
- Se quiser publicar depois (link acessível de qualquer aparelho, com sincronização), me avise — dá para reaproveitar este mesmo layout e adicionar um backend, como foi feito no app de Controle de Pagamentos.

## Identidade visual

- Logo oficial da Sellmed em destaque no cabeçalho (`assets/logo.svg`).
- Paleta: azul-marinho `#0C2F79`, teal `#1EA4A8` e verde `#73CC6E` (cores extraídas da logo/materiais institucionais da Sellmed), com a barra de destaque em degradê navy → teal → green.
- Tipografia Montserrat (títulos) e Inter (corpo de texto).
