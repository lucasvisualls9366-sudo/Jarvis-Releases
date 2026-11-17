# JARVIS 2.1.269 — validação

Correção do visual do Amigo 2 fora de chamadas e da lateral de amigos/grupos, conforme referências aprovadas. A janela principal volta a usar a moldura nativa com —, □ e X, sem botões personalizados duplicados.

Verificações obrigatórias: tipagem da aplicação, build, Chromium com duas sessões WebRTC nos dois sentidos, grupos e reentrada, presença listada individualmente abaixo do grupo, entrada sem microfone, mídia e processamento de áudio. Capturas também antes da chamada: fundo preto, fonte legível, AMIGOS/GRUPOS e busca na engrenagem.

Preservados: chamadas, compartilhamento e miniaturas, cartões sem transmissão, engrenagem, chat recolhível, anexos, áudio, reações, convites de jogos, histórico e demais módulos JARVIS. Sem alteração de banco nesta versão. O lint global legado apresenta falha interna do TypeScript, já documentada; a tipagem específica da aplicação e o build permanecem obrigatórios.

A eficácia acústica de eco/ruído depende do equipamento; esta revisão modifica apresentação e controles da janela.

## Publicação confirmada

- CI Windows: https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/actions/runs/44180632332 — concluído com sucesso.
- Release pública: https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/releases/tag/v2.1.269
- Fonte compilada e tag privada v2.1.269: `e227f75791ab4e714999a4eb766b3afa0fa60a2a`.
- Instalador baixado: 289598526 bytes; cabeçalhos MZ/PE válidos. Manifesto e blockmap disponíveis.
- SHA-512 confere com latest.yml; SHA-256 confere com o asset GitHub: `fbfa07556b5d4e4e4e638e154b8d8bd5f00004a757dd5a744df3e37516c49ea3`.
- Testes obrigatórios passaram: tipagem da aplicação, build, layout fora de chamada, fundo preto, fonte legível, chat à direita, lista individual de participantes na lateral, configurações/edição de grupo na engrenagem, chamadas A→B e B→A, grupo/reentrada, ausência de microfone, mídia, áudio e regressões dos demais módulos.
- Moldura nativa restaurada por `BrowserWindow.frame: true`; teste também rejeita regressão para janela sem moldura. Controles HTML duplicados removidos. Capturas do navegador mostram o conteúdo, sem a moldura nativa do Windows.
- Lint global opcional: permanece o erro interno legado `Debug Failure. False expression.` do TypeScript; tipagem específica da aplicação e compilações obrigatórias passaram.
