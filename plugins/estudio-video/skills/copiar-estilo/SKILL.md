---
name: copiar-estilo
description: Copia o estilo de edição de um vídeo de referência (a Vera, analista de conteúdo do Time Nautic). Assiste o vídeo da pasta ~/Estúdio Nautic/3 - Referências, mede legenda (fonte aproximada, tamanho, cor, destaque, posição, animação), ritmo (tempo médio de plano, zooms, trocas), efeitos, música e estrutura (gancho, corpo, chamada), e grava um estilo reutilizável em 5 - Estilos. Use quando o pedido do Estúdio vier com o estilo "Copiar uma referência", ou o usuário disser "copia o estilo desse vídeo", "quero igual a esse Reel", "faz no estilo desse aqui".
---

# Copiar estilo (v1.2.0)

Copie **o jeito**, nunca o conteúdo: não reutilize música, imagem, texto, marca ou rosto de quem fez a referência.

## Passos
1. Pegue o vídeo mais recente de `~/Estúdio Nautic/3 - Referências` (ou o link que o usuário mandou; baixe com `yt-dlp` se for público e o uso for estudo).
2. **Medir:**
   - Trocas de plano: `ffmpeg -i ref.mp4 -vf "select='gt(scene,0.25)',showinfo" -f null - 2>&1 | grep pts_time` → tempo médio e mínimo de plano.
   - Quadros a cada 0,5 s nos primeiros 3 s e a cada 2 s depois: `ffmpeg -i ref.mp4 -vf fps=2 -t 3 g_%02d.png` e `fps=0.5`. Leia as imagens.
   - Transcrição (`npx hyperframes transcribe`) para ver o gancho, quantas palavras por legenda e a chamada final.
   - Volume e música: `ebur128`; existe trilha? batida marcada? efeitos nos cortes?
3. **Descrever a receita** no mesmo formato da tela do Estúdio:
   - legenda: fonte (a mais parecida entre Inter, Montserrat, Poppins, Bebas Neue, Playfair), peso, tamanho em px (para 1080×1920), cor, destaque, caixa, posição y, animação, palavras por vez;
   - ritmo; efeitos (nomes do catálogo: digital zoom, zoom-through cut, glass type, chip row, checklist, blackout, phone mockup, freeze + label, texto atrás da pessoa, B-roll em painel...); som; estrutura (gancho, corpo, chamada, duração).
4. Grave `~/Estúdio Nautic/5 - Estilos/<nome-curto>.md` com a receita, a data, de onde veio e 3 quadros de exemplo (`<nome>-1.png`...).
5. Mostre ao usuário a receita em 6 linhas e pergunte só: "uso este estilo agora?". Depois a skill `estudio-nautic` aplica.

## Da próxima vez
Se o pedido citar um estilo que já está em `5 - Estilos`, use a receita gravada sem medir de novo.
