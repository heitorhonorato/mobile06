# Contexto do projeto — Separação de Pedidos

## O que é
Ferramenta interna para uma empresa de suplementos de academia. O usuário faz a
separação física dos pedidos coletados pelo Mercado Livre e Shopee. Para cada
leva de pedidos, ele recebe uma ou mais Notas Fiscais Eletrônicas (NF-e) em PDF.

O site resolve dois problemas:
1. Gerar a lista de quanto separar de cada produto, a partir das notas em PDF.
2. Conferir cada nota antes do envio, marcando como conferida.

## Como funciona hoje
- Um único arquivo `index.html`, com CSS e JavaScript embutidos (sem build,
  sem framework, sem backend).
- PDF.js (via CDN) lê o texto dos PDFs direto no navegador — nenhum arquivo
  sai do celular/computador do usuário. Também aceita o HTML das notas
  baixado do ERP da Olist (lido com DOMParser, também no navegador).
- As notas são separadas pelo título "DANFE" (não por página). A quantidade
  vem da coluna QTD da tabela de produtos (CÓD. DESCRIÇÃO UN QTD ...), e o
  produto é reconhecido por palavras-chave na descrição. Se a tabela não
  estiver nesse formato, o site usa só as palavras-chave (quantidade 1) e
  marca a nota para conferir. Os campos de quantidade continuam editáveis.
- Progresso da conferência (checkboxes) é salvo em `localStorage`, para não
  perder o andamento se a página recarregar.
- Hospedado de graça no GitHub Pages.

## Catálogo de produtos (pode mudar — sempre confirmar com o usuário antes de alterar)
- Whey Baunilha / Morango / Chocolate 900g
- Creatina 300g / 500g / 1000g
- Pré Treino 300g — Maçã Verde / Frutas Vermelhas
- Coqueteleira 700ml
- Glutamina 300g
- Beta Alanina 300g
- Beta Alanina 1kg
- Magnésio 300g
- Vandal King Jump 300g — Blue Razz / Limonade
- Termogênico 300g
- Kit Especial (Whey Pro + Creatina 100g + coqueteleira diferente do kit normal)
- Kit Creatina 1kg = 2× Creatina 500g
- Kit 600g = 2× Creatina 300g

### Regras de kits e equivalências (confirmadas pelo usuário)
- Kits nunca entram na lista como "kit": são desmontados e cada peça soma
  1 unidade no produto correspondente.
- "Kit Suplemento Whey Protein + Creatina Pura + Coqueteleira Shaker - <sabor>"
  é o Kit Especial (só existe na Shopee) = 1 Whey Pro do sabor + 1 Creatina
  100g + 1 coqueteleira do kit. Esses três itens só existem dentro do kit.
- Os outros kits já vêm na nota como produtos unitários normais.
- "Magnesio Inositol ... 210g Maracujá" na nota = o Magnésio do catálogo.
- Não existe creatina de 2kg no estoque: "Creatina ... 2kg" = 2 Creatinas 1kg.

## Novas funcionalidades
- **Aba de Início:** ao abrir o site, escolha se as notas são da Shopee ou Mercado Livre.
  A escolha é salva no relatório.
- **Relatório:** mostra todas as notas processadas, a data e hora da leva, produtos
  separados e quaisquer problemas encontrados (produtos fora do catálogo, tabelas
  não reconhecidas, etc). Trazir erros para a conversa para resolvermos.
- **Sistema de erros:** quando o site não conseguir reconhecer um produto ou a tabela
  estiver num formato inesperado, registra exatamente qual nota teve o problema
  e mostra no relatório.

## Restrições técnicas
## Restrições técnicas (não mudar sem avisar)
- Continuar em **um único arquivo HTML** — sem servidor, sem serviço pago,
  sem etapa de build. Precisa funcionar hospedado como página estática pura.
- Todo processamento (leitura de PDF, extração de texto, cálculo) acontece
  no navegador do usuário.
- Interface sempre em português, pensada para uso no celular (botões grandes,
  fácil de tocar, fonte legível).
- Se algo não puder ser feito automaticamente (ex: nota fiscal escaneada como
  imagem, sem texto), mostrar um aviso claro — nunca falhar silenciosamente.

## Sobre o usuário
- Sem experiência prévia em programação — está aprendendo aos poucos.
- Prefere explicações simples e diretas, sem jargão técnico sem explicação.
- Antes de qualquer mudança estrutural grande (trocar de único arquivo para
  múltiplos, adicionar backend, mudar de hospedagem), explique o motivo e
  peça confirmação antes de fazer.
- Este é um dos primeiros projetos de um plano maior de criar sites com IA
  (para uso próprio e depois para pequenos negócios) — trate como um projeto
  de aprendizado, não só de entrega.

## Como trabalhar aqui
- Ao terminar uma alteração, explique em 2-3 frases simples o que mudou e
  por quê, como se estivesse explicando para alguém que nunca programou.
- Sempre que possível, teste mentalmente o fluxo (upload de PDF → lista →
  conferência) antes de considerar a tarefa concluída.
- Ao commitar/subir para o GitHub, use mensagens de commit curtas e claras
  em português (ex: "corrige reconhecimento de creatina 1kg").
