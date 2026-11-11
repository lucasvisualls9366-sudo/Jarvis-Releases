# JARVIS — downloads e atualizacoes oficiais

Este repositorio publico distribui instaladores e manifestos de atualizacao do JARVIS. **O codigo-fonte permanece privado** no repositorio `lukasvisualls-dev/Jarvis`.

## Baixar a versao oficial

- [Ultima versao do JARVIS (com instalador Windows)](https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/releases/latest)
- [Manifesto de autoatualizacao (`latest.yml`)](https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/releases/latest/download/latest.yml)
- [Historico de versoes](https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/releases)

## Compilacao Windows na nuvem — sem PC e sem gastos

O workflow [JARVIS - Build Windows gratuito e atualizacoes](.github/workflows/jarvis-windows-cloud.yml) usa `windows-latest` **padrao em repositorio publico**, modalidade gratuita do GitHub Actions. O codigo e obtido do repositorio privado somente durante o build em um runner descartavel; o codigo-fonte e tokens nao sao colocados neste repositorio.

**Segredos obrigatorios em Settings > Secrets and variables > Actions deste repositorio:**

- `JARVIS_SOURCE_TOKEN`: token fine-grained da conta `lukasvisualls-dev`, escopo limitado a **Jarvis**, permissao **Contents: Read-only**.
- Para **publicar** versoes novas, configurar tambem `VITE_JARVIS_LEGAL_PROVIDER_NAME`, `VITE_JARVIS_LEGAL_PROVIDER_REGISTRATION`, `VITE_JARVIS_LEGAL_PROVIDER_ADDRESS` e `VITE_JARVIS_LEGAL_CONTACT` com os valores reais ja aprovados para o aplicativo. Publicacao sem esses valores e bloqueada.

A publicacao neste proprio repositorio usa o `GITHUB_TOKEN` nativo do GitHub Actions com `contents: write`; **nao e necessario criar `JARVIS_RELEASES_TOKEN`** aqui.

**Teste inicial seguro:** Actions > JARVIS - Build Windows gratuito e atualizacoes > Run workflow. Manter a opcao `publicar` desmarcada. O teste compila o instalador sem publicar, substituir releases ou armazenar artefatos publicos.

**Atualizacao automatica:** a cada 12 horas, um job simples verifica a versao no codigo privado. Somente quando `package.json` tem uma versao superior a ultima release e existe `release-trigger/VERSAO.md`, roda validacoes, compila Windows e publica os tres arquivos apos verificacoes. Jamais substitui a release anterior ou publica a mesma versao. Ate os segredos serem configurados, o monitoramento nao compila nem publica.

**Seguranca:** nao publicar tokens, codigo privado nem dados pessoais em commits ou logs. Nunca habilitar jobs que usem segredos em eventos de pull requests de terceiros. Logs das execucoes deste repositorio publico sao acessiveis a terceiros, mesmo quando o codigo-fonte utilizado e privado.

**Validacao concluida em 2026-11-11:** a compilacao real Windows-2022 terminou com [Success (run 43100759712)](https://github.com/lucasvisualls9366-sudo/Jarvis-Releases/actions/runs/43100759712). Testes, empacotamento e verificacoes do instalador passaram. Publicacao permaneceu desativada, preservando a v2.1.246. O workflow legado no repositorio privado agora e somente manual. Antes de formatar, realizar o [backup local do Windows](https://github.com/lukasvisualls-dev/Jarvis/blob/main/docs/FORMATACAO_SEGURA.md). Builds agendados somente publicam versoes superiores com notas e dados legais configurados; mudancas comuns sem aumento de versao nao publicam release.
