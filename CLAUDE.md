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
  sai do celular/computador do usuário.
- A extração de produto/quantidade é feita por correspondência de palavras-
  chave no texto da nota (não por posição fixa na página), porque o layout
  das notas varia. Por isso os campos de quantidade na lista final são
  editáveis — é um "chute" heurístico, não uma leitura garantida.
- Progresso da conferência (checkboxes) é salvo em `localStorage`, para não
  perder o andamento se a página recarregar.
- Hospedado de graça no GitHub Pages.

## Catálogo de produtos (pode mudar — sempre confirmar com o usuário antes de alterar)
- Whey Baunilha / Morango / Chocolate 900g
- Creatina 300g / 500g / 1000g
- Pré Treino 300g — Maçã Verde / Frutas Vermelhas
- Coqueteleira 700ml
- Glutamina e Beta Alanina 300g
- Beta Alanina 1kg
- Magnésio 300g
- Vandal King Jump 300g — Blue Razz / Limonade
- Termogênico 300g
- Kit Especial (Whey Pro + Creatina 100g + coqueteleira diferente do kit normal)

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
