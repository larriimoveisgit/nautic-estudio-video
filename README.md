# Estúdio de Vídeo Nautic (plugin do Claude Code)

Edite Reels, TikTok e Shorts conversando com o Claude Code: corta pausas e erros, limpa o som, legenda no estilo escolhido, coloca imagens por cima, efeitos, música, capa e versões por rede. Antes de entregar, um revisor confere tudo com números.

Feito pela [Nautic Negócios Imobiliários](https://nauticnegociosimobiliarios.com.br) para corretores. Corretores da Nautic montam o pedido na tela **Estúdio de Vídeo** do portal e colam no Claude Code.

## Instalar
```
/plugin marketplace add larriimoveisgit/nautic-estudio-video
/plugin install estudio-video@nautic
```
Precisa de: Claude Code (plano Pro ou superior), ffmpeg, Node 22+ e o HyperFrames (`npx skills add heygen-com/hyperframes`). A skill confere e instala o que faltar.

## O que vem
| Skill | Faz |
|---|---|
| `estudio-nautic` | Editor: recebe o pedido, mostra os cortes, edita, entrega em 1080×1920 |
| `revisor-de-video` | Confere gancho, legenda, zona segura, volume (−14 LUFS), resolução, fato duro |
| `copiar-estilo` | Mede o estilo de um vídeo de referência e grava uma receita reutilizável |
| `roteiro-de-video` | Gancho, provas e chamada antes de gravar |

E 16 receitas de estilo em `plugins/estudio-video/estilos/` (copiadas para `~/Estúdio Nautic/5 - Estilos`).

Pastas que o Estúdio cria: `~/Estúdio Nautic/0 - Marca`, `1 - Brutos`, `2 - Imagens`, `3 - Referências`, `4 - Prontos`, `5 - Estilos`.

## Regras
Nunca sobrescreve o original, não inventa preço nem prazo, não promete valorização, não publica nada sozinho. Estilo de referência copia o jeito, nunca música, imagem ou marca de quem fez.

Este repositório é gerado automaticamente a partir do repositório da Nautic (`tools/estudio/gerar_pacote.mjs`). Licença MIT.
