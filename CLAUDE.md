# Site — Marana Ali · Fisioterapia

## Regra nº 1: leia o briefing antes de qualquer tarefa

Antes de executar qualquer pedido neste projeto, leia [BRIEFING.md](BRIEFING.md). Ele é a fonte da verdade sobre o que a cliente quer. Não faça nada que contradiga o briefing, e não acrescente seções, funcionalidades ou informações que não estejam nele ou que não tenham sido pedidas explicitamente pelo usuário.

Se um pedido conflitar com o briefing, aponte o conflito e pergunte antes de seguir.

## Nunca inventar dados

O briefing deixa várias coisas em aberto. Enquanto não forem definidas, use um marcador visível entre colchetes (ex.: `[a definir]`) em vez de inventar:

- Endereço do espaço, e-mail, Instagram/redes sociais (WhatsApp já definido: +55 84 9620-8586)
- Valores das sessões (ainda não decidido se aparecem no site)
- Link da planilha de agenda (`AGENDA_CSV`) — ver "Agenda de horários" abaixo
- Nº do CREFITO, logotipo, paleta oficial, fotos
- Depoimentos, números de pacientes, avaliações, estatísticas
- Política de cancelamento/reagendamento

## Decisões que já valem

- Conversão principal: conhecer os serviços → falar pelo WhatsApp. A marcação é concluída no WhatsApp, não no site (sem agendamento automático, sem pagamento online, sem confirmação automática).
- Agenda de horários (decidido em 30/10/2026, revê a Q22 do briefing; aprovação da cliente pendente): o site mostra os horários livres e o paciente escolhe um, mas a reserva só vale após confirmação no WhatsApp.
- Serviços: Gerontologia, Ortopedia e Traumatologia, Terapia Manual. Nenhum tem destaque sobre os outros.
- Atendimento individual, ~50 min, no espaço próprio ou em domicílio (Zona Sul de Natal; Leste e Oeste conforme distância). Preço difere entre os dois formatos.
- Uma única profissional: Marana Ali — Fisioterapeuta, UFRN, especialização em Fisioterapia Gerontológica.
- Sem convênios. Público: adultos e idosos.
- Marca: diferenciada, agradável, atenciosa, detalhista. Evitar qualquer ar de baixa qualidade ou amadorismo.

## Estrutura do arquivo HTML

`Marana Ali — Landing Page – Landing Page — Desktop.html` é um bundle exportado (React + dc-runtime). O conteúdo real da página não está no HTML visível:

- A linha que segue `<script type="__bundler/template">` contém o template da página como uma string JSON (com `</` escapado como `</`).
- Dentro do template: o markup fica em `<x-dc>…</x-dc>` (bindings `{{ }}`, `<sc-if value>`, `<sc-for list as>`, eventos `sc-camel-on-click`, `<select>` vira `<sc-raw-select>`), e a lógica fica em `<script type="text/x-dc" data-dc-script>` numa `class Component extends DCLogic` com `renderVals()`.
- Fotos ficam em `imagens/` (WebP otimizado) e são referenciadas por caminho relativo: a pasta precisa ser publicada junto com o `index.html`.
- Para editar: decodificar essa linha com `JSON.parse`, alterar, e regravar com `JSON.stringify(...).replace(/<\//g, '<\\u002F')`. Não mexer no manifest (fontes/React em base64).

## Agenda de horários

- Grade: segunda a sexta, sessões de hora em hora das 7h às 19h (50 min + 10 de intervalo, até as 20h).
- Em domicílio a sessão ocupa 1h15: só é oferecida se a hora seguinte também estiver livre, e a última é às 18h.
- Os horários ocupados vêm de uma planilha Google que só a fisioterapeuta edita, publicada como CSV no link `AGENDA_CSV` (topo do script). A planilha lista só exceções: `Data | Hora | Situação` (hora em branco ou "dia todo" bloqueia o dia). Domicílio marcado = marcar as duas horas como ocupadas.
- A planilha é pública para leitura: nunca colocar nome ou dados de paciente nela.
