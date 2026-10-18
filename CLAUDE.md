# Site — Marana Ali · Fisioterapia

## Regra nº 1: leia o briefing antes de qualquer tarefa

Antes de executar qualquer pedido neste projeto, leia [BRIEFING.md](BRIEFING.md). Ele é a fonte da verdade sobre o que a cliente quer. Não faça nada que contradiga o briefing, e não acrescente seções, funcionalidades ou informações que não estejam nele ou que não tenham sido pedidas explicitamente pelo usuário.

Se um pedido conflitar com o briefing, aponte o conflito e pergunte antes de seguir.

## Nunca inventar dados

O briefing deixa várias coisas em aberto. Enquanto não forem definidas, use um marcador visível entre colchetes (ex.: `[a definir]`) em vez de inventar:

- Endereço do espaço, número de WhatsApp, e-mail, Instagram/redes sociais
- Valores das sessões (ainda não decidido se aparecem no site)
- Dias e horários de atendimento — a cliente **prefere não divulgar** (Q22)
- Nº do CREFITO, logotipo, paleta oficial, fotos
- Depoimentos, números de pacientes, avaliações, estatísticas
- Política de cancelamento/reagendamento

## Decisões que já valem

- Conversão principal: conhecer os serviços → falar pelo WhatsApp. A marcação é concluída no WhatsApp, não no site (sem agendamento automático, sem pagamento online, sem confirmação automática).
- Serviços: Gerontologia, Ortopedia e Traumatologia, Terapia Manual. Nenhum tem destaque sobre os outros.
- Atendimento individual, ~50 min, no espaço próprio ou em domicílio (Zona Sul de Natal; Leste e Oeste conforme distância). Preço difere entre os dois formatos.
- Uma única profissional: Marana Ali — Fisioterapeuta, UFRN, especialização em Fisioterapia Gerontológica.
- Sem convênios. Público: adultos e idosos.
- Marca: diferenciada, agradável, atenciosa, detalhista. Evitar qualquer ar de baixa qualidade ou amadorismo.

## Estrutura do arquivo HTML

`Marana Ali — Landing Page – Landing Page — Desktop.html` é um bundle exportado (React + dc-runtime). O conteúdo real da página não está no HTML visível:

- A linha que segue `<script type="__bundler/template">` contém o template da página como uma string JSON (com `</` escapado como `</`).
- Dentro do template: o markup fica em `<x-dc>…</x-dc>` (bindings `{{ }}`, `<sc-if value>`, `<sc-for list as>`, eventos `sc-camel-on-click`, `<select>` vira `<sc-raw-select>`), e a lógica fica em `<script type="text/x-dc" data-dc-script>` numa `class Component extends DCLogic` com `renderVals()`.
- Para editar: decodificar essa linha com `JSON.parse`, alterar, e regravar com `JSON.stringify(...).replace(/<\//g, '<\\u002F')`. Não mexer no manifest (fontes/React em base64).
