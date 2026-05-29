# Sistema de Compras

Ferramenta web (um único arquivo HTML) para gestão de insumos, sugestão de compra e **follow-up de entregas**.

## Como hospedar (GitHub Pages)

1. Suba `sistema_compras_4.html` e `backup.json` para o repositório.
2. Em **Settings → Pages**, ative o GitHub Pages apontando para a branch (ex.: `main`, pasta `/root`).
3. Acesse pela URL gerada (ex.: `https://SEU-USUARIO.github.io/SEU-REPO/sistema_compras_4.html`).

> Importante: a carga automática do `backup.json` só funciona quando o sistema está **hospedado** (http/https). Se você abrir o arquivo direto do disco (`file://`), o navegador bloqueia a leitura do `backup.json` por segurança — nesse caso, use o botão "Restaurar backup".

## Como os dados funcionam

- Os dados ficam salvos **no navegador de cada pessoa** (IndexedDB). O Git compartilha o *programa* e o *backup*, não um banco de dados ao vivo.
- O arquivo `backup.json` no repositório é a **fonte compartilhada**: ao abrir, o sistema carrega o último backup commitado.

## Fluxo de backup (recomendado para uso em equipe)

1. Abra o sistema (ele já carrega o `backup.json` mais recente do repositório).
2. Faça as alterações (importar planilha do SAP, marcar entregas, observações, etc.).
3. Vá em **Atualizar dados → Salvar backup pro Git** — baixa o arquivo `backup.json`.
4. Substitua o `backup.json` do repositório por esse e faça `commit` + `push`.

Na próxima vez que qualquer pessoa abrir, o sistema carrega o estado novo.

- Se o navegador estiver **vazio** (pessoa nova / outro computador), o `backup.json` é carregado automaticamente.
- Se já houver dados locais e existir um `backup.json` **mais recente** no repositório, aparece um aviso no topo perguntando se quer carregar (nunca sobrescreve sozinho).

### Atenção (não é tempo real)

Se duas pessoas editam ao mesmo tempo, quem salvar por último "ganha". Para evitar perder trabalho, combinem uma rotina simples: **puxar do git → editar → exportar → commitar**. Para edição simultânea de verdade, seria necessário um backend (ex.: Supabase/Firebase).

## Follow-up de entregas

- Importa o relatório de pedidos do SAP e mostra apenas itens com **Qtde Aberta > 0** do comprador **Lucas Santos**.
- Permite ajustar data de entrega, marcar entrega total/parcial e registrar observações.
- As anotações são guardadas por **Nº do Pedido + Cód. Item** e **não são apagadas** ao subir uma planilha nova do SAP — os dados-base são atualizados e suas anotações permanecem.
- O botão "Exportar planilha atualizada" gera um Excel com os dados + suas anotações, que também pode ser recarregado depois.

## Arquivos

- `sistema_compras_4.html` — o sistema completo.
- `backup.json` — backup compartilhado dos dados (atualize via commit).
