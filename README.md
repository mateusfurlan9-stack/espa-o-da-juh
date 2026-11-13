# Espaço da Juh — Agenda

Clientes: `/`. Administração: `/admin`. Não há link para o painel na página das clientes.

## Acesso

O servidor usa a identidade validada pelo Sites/ChatGPT e confere o e-mail em cada operação administrativa. Até configurar a conta da Juh, somente a conta proprietária definida na variável `ADMIN_BOOTSTRAP_EMAIL` pode administrar. Em “Acesso da Juh”, repita o e-mail da conta ChatGPT dela para transferir o acesso. A conta anterior perde a permissão. É preciso liberar também o acesso dela na audiência do Site se ele estiver privado. Nunca compartilhar senha do ChatGPT.

## Uso

- Bloquear dia: escolher data e salvar com “Todos os horários (dia inteiro)” marcado.
- Bloquear horários: selecionar um ou vários botões de intervalos de uma hora e salvar. Para outros intervalos, escolher “Informar outro intervalo” e preencher início/fim.
- Atendimento confirmado pelo WhatsApp: selecionar esse tipo e cadastrar o intervalo completo. Pedidos pelo WhatsApp não reservam automaticamente e não são sincronizados com a InfinitePay.
- Remover ou cancelar registros libera os horários se não houver outro bloqueio. “Desfazer” restaura o registro.
- A disponibilidade considera quarta a sábado, 9h–17h, e o fuso America/Sao_Paulo. Serviços com duração informada consideram a duração na seleção. Nos três novos serviços sem duração informada, o calendário oferece horários de início em intervalos de 15 minutos; a duração precisa ser combinada antes da confirmação e registrada integralmente no painel.

Os dados persistem em D1. A API pública retorna apenas horários livres, sem nomes nem notas. As verificações são feitas no servidor. O cliente atualiza a disponibilidade a cada 30 segundos e novamente antes de gerar a mensagem do WhatsApp. Bloquear um horário não envia mensagem a clientes.

## Desenvolvimento

`npm test` executa os testes com SQLite em memória. `npm run build` gera um Worker ESM com os arquivos públicos embutidos. A migração em `drizzle` é aplicada pelo Sites no deploy. `scripts/dev.mjs` cria uma base separada em `.preview` e usa uma identidade fictícia exclusivamente para a prévia local; esse servidor não é o Worker publicado.

## Seleção de vários serviços

A cliente pode marcar vários serviços e desmarcar a qualquer momento. A seleção permanece ao trocar de categoria e ao voltar da escolha de horário. O resumo mostra o total pela soma dos preços do catálogo; a mensagem de WhatsApp lista cada serviço e seu preço. A disponibilidade considera a soma das durações cadastradas, mantendo a confirmação manual pela Juh.
