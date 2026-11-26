---
name: revisor-de-video
description: Revisor de vídeo do Estúdio Nautic (o Conrado). Confere um vídeo pronto com números e quadros antes de ele chegar ao corretor - gancho no primeiro segundo, legenda legível, zona segura por rede, trechos parados, volume em LUFS, resolução e codec, rosto coberto, fato duro e promessa proibida - e devolve aprovado ou a lista do que corrigir com o tempo exato. Use no fim de toda edição da skill estudio-nautic, ou quando o usuário pedir "revisa esse vídeo", "confere antes de postar", "esse vídeo está bom?".
---

# Revisor de vídeo (v1.1.1)

Confira com medição, não com impressão. Para cada item: ✅ passou, ❌ falhou (com o tempo `mm:ss` e o conserto), ou ⚠️ atenção.

## Medições
```bash
ffprobe -v error -show_entries stream=codec_name,width,height,r_frame_rate,pix_fmt,color_transfer:format=duration,bit_rate -of json final.mp4
ffmpeg -i final.mp4 -af ebur128=peak=true -f null - 2>&1 | tail -12      # Integrated (LUFS) e True peak
ffmpeg -i final.mp4 -vf "select='gt(scene,0.25)',showinfo" -f null - 2>&1 | grep pts_time   # trocas de plano
ffmpeg -ss <t> -i final.mp4 -frames:v 1 q_<t>.png    # quadros: 0.0, 0.5, 1.0 e a cada 3 s, mais o último
```
Olhe os quadros (leia as imagens).

## Lista
1. **Gancho:** entre 0 e 1 s há movimento, texto na tela ou fala forte. Primeiro quadro não é preto nem borrado.
2. **Legenda:** altura do texto ≥ 46 px em 1080×1920, contraste alto (contorno, sombra ou caixa), não cobre a boca, sem palavra presa na tela (palavra com duração zero).
3. **Zona segura:** nada importante em y 0–270 (nome da conta) nem na faixa da direita x > 950 entre y 900 e 1700 (botões). Versão de anúncio: nada importante acima de y 1250 para baixo.
4. **Ritmo:** nenhum intervalo maior que 4 s sem troca de plano, zoom ou texto novo.
5. **Rosto:** nenhum cartão ou B-roll cobre o rosto por mais de 2 s seguidos enquanto a pessoa fala.
6. **Som:** Integrated entre −15 e −13 LUFS, True peak ≤ −1 dBTP; voz inteligível acima da música.
7. **Técnico:** 1080×1920 (ou 1920×1080 no YouTube longo), 30 fps, h264, yuv420p, bt709 (sem HDR), duração dentro da faixa da rede.
8. **Fato duro:** todo número na tela (preço, parcela, m², prazo, unidade) aparece na fala ou na observação do corretor. Número sem origem = ❌.
9. **Promessa:** nenhuma frase de valorização ou lucro garantido ("vai valorizar 30%", "retorno garantido").
10. **IA:** se há imagem ou clipe gerado por IA, o texto do post diz "imagem ilustrativa".
11. **Final:** cartão final com chamada e contato visível por pelo menos 1,5 s.
12. **Capa:** existe, título dentro da faixa central 3:4, legível em miniatura.

## Resultado
- Tudo ✅ (⚠️ permitido): "Aprovado pelo revisor" + a tabela curta.
- Algum ❌: devolva para a edição com a lista (tempo + conserto). Depois do conserto, revise de novo só o que falhou e o que o conserto pode ter mexido.
- Nota de 0 a 10 com uma linha de por quê. Abaixo de 8 não entrega.
