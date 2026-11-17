# Validação JARVIS 2.1.268

## Escopo

Amigo 2 no layout preto aprovado, dois estados de participantes, engrenagem centralizando configurações, ícones sem texto sobreposto, chat recolhível, chamadas e presença em grupo. Imagens de referência em docs/amigo2; o editor ilustrado nas referências é apenas exemplo de conteúdo compartilhado.

## Verificações

- Tipagem da aplicação: `npx tsc -p tsconfig.app.json`; build Vite e servidor esbuild.
- Duas sessões Chromium isoladas, React e WebRTC reais: ligação A → B e B → A, toque de recebimento, atendimento, áudio, tela e áudio da tela, chat, fim remoto, limpeza de mídia e mudanças de processamento. Apenas transporte de documentos/contas de teste e fontes de captura são simulados; não usa contatos reais.
- Sem microfone nas duas pontas: chamada recebida e atendida para escuta; grupo conectado, saída e reentrada. Dispositivo salvo removido, incompatibilidade de constraints e permissão negada também cobertos.
- Grupo: convite, dois peers conectados, presença dos dois, saída e reentrada na mesma sala com novo identificador de sessão.
- Eco/ruído: switches alteram `getSettings().echoCancellation` e `noiseSuppression` da entrada ativa, preservam mute e encerramento interrompe tracks. Não foi realizado ensaio acústico físico com os alto-falantes/microfone do usuário; flags ativas não medem redução em dB.
- Layout desktop/móvel, miniaturas pequenas durante transmissão, cartões grandes sem transmissão, área ampliada ao recolher chat e ícone de transmissão sem texto. Capturas de execução em `test-results/friends`, publicadas como artefato de CI.
- Recuperação de candidatos ICE perdidos, reentrada, qualidade adaptativa, 10 participantes, atualizações manuais e controles da janela. Regressões adicionais executadas pelo workflow Windows antes da publicação.
- Migração `20261117200623_amigo2_call_presence.sql` aplicada: sala única por grupo, autorização por associação, bloqueio transacional e permissões de execução apenas autenticadas; RLS preservado.

## Limites

Conexão WebRTC depende das redes e dispositivos. Ensaios locais não garantem travessia de todos os NAT/firewalls nem ausência absoluta de latência; redes restritas podem requerer relay TURN. O lint global legado tem falha interna do TypeScript 5.8.3 documentada na versão anterior; a tipagem específica da aplicação e o build são obrigatórios.

Publicação exige workflow Windows concluído, instalador, blockmap e latest.yml na release pública, com conferência de disponibilidade e checksum.

Uma tentativa adicional de consultar o estado do banco em 17/11 não foi executada: a revisão automática de aprovação atingiu o limite de uso. A aplicação e a conferência da migração haviam sido concluídas antes; a repetição adicional não é apresentada como executada.

## Publicação confirmada

- Workflow Windows concluído com sucesso: https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/actions/runs/44174764869
- Release pública: https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/releases/tag/v2.1.268
- Fonte compilada e tag privada v2.1.268: `f43a035d45256cbe74e5a6c7329da2c61f724f58`.
- Instalador baixado da release: 289585638 bytes; cabeçalhos MZ/PE válidos. `latest.yml` e blockmap disponíveis.
- SHA-512 do arquivo baixado confere com o manifesto; SHA-256 confere com o digest do asset no GitHub: `dcec9e93fdcba6f7c807241248e9ff208660122b89287513d4445c1c1ddf8239`.
- Testes Windows obrigatórios concluídos, incluindo chamadas nos dois sentidos, eco/ruído ao vivo, voz detectada, grupo com reentrada, ausência de microfone, mídia, atualizações, autenticação, jogos e Conversor com FFmpeg/HEIC reais. A tentativa local adicional de formatos sem FFmpeg instalado falhou por ausência do binário; os mesmos testes passaram no Windows com o motor instalado.
- O lint global opcional continua com `Debug Failure. False expression.` do TypeScript, como documentado anteriormente. A tipagem obrigatória da aplicação e as compilações passaram.
