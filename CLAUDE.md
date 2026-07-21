# Inventário Rio Pomba — instruções para o Claude Code

Site de consulta de centros de custo (SISERGE) do Campus Rio Pomba (IF Sudeste MG).
Árvore hierárquica publicada via GitHub Pages, atualizada por GitHub Actions.

## Arquivos (NÃO apagar template.html, gerar.py nem a .xlsx)
- `template.html` — aparência/comportamento (editar SÓ se pedirem mudança visual)
- `gerar.py` — converte a .xlsx em index.html e VALIDA os dados
- `index.html` — GERADO. Nunca editar à mão.
- `.xlsx` — os dados. Só pode existir UMA planilha no repo (o robô falha de propósito se houver duas).

## Estrutura da planilha (1 aba, sem células mescladas)
- Colunas A–D = níveis 1–4 da árvore; coluna E = código.
- Célula vazia em A–D herda o nível anterior; o código fica no último nível preenchido.
- Cada linha tem texto em UMA única coluna A–D. Nível N exige um pai no nível N-1.
- Sem duplicatas, sem órfãos.

## Fluxo obrigatório para QUALQUER mudança de dados
1. Editar a .xlsx com openpyxl (preservar nome do arquivo e a aba única).
2. Rodar `python gerar.py` LOCALMENTE. Se falhar, ler a linha/motivo, corrigir na planilha e repetir. NÃO subir dados inconsistentes.
3. Só depois: `git add -A && git commit -m "<descrição curta do que mudou>" && git push`.
4. Informar ao usuário para conferir a aba Actions (deve ficar verde) e testar em aba anônima.

## Sistema de cores (só se mexer no template.html — opção C, em produção)
- Nível 1 #3FA46E · Nível 2 #9FCBB4 · Nível 3 #AFC9DB · Nível 4 #D9C2B0
- Folha (nó com código): fundo âmbar #FBEFCB + faixa lateral esquerda na cor do nível.
- Pílula do código: vermelho #C4161C.
- Busca: nó final do resultado com borda âmbar-escura #d9b23c.

## Segurança (o gerar.py cuida sozinho — não quebrar)
CSP com hashes SHA-256 recalculados a cada build, render só via textContent,
sanitização no JS, frame-busting, referrer no-referrer, logo em base64.

## Base validada de referência: 411 nós / 365 códigos.
## Pendência conhecida: conferir 70010 "JARGAS" (provável "VARGAS").
