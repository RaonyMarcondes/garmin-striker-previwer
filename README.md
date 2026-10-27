# Simulador de frequências do sonar Garmin Striker Vivid 4cv

Simulador interativo que mostra como cada frequência do **Garmin Striker Vivid 4cv** com o transdutor **GT20-TM** enxerga o fundo, a estrutura e os peixes debaixo de um caiaque de pesca. A cena 3D e a tela do sonar são geradas a partir do mesmo mundo simulado. Assim dá para ver, lado a lado, o feixe atingindo o fundo e a imagem que ele produz.

Roda inteiro no navegador: HTML, CSS, JavaScript e WebGL ([three.js](https://threejs.org)), sem build e sem back-end.

## O que dá para fazer

- **Trocar a frequência** e ver o efeito na hora:
  - Sonar tradicional: CHIRP 77 kHz, CHIRP 200 kHz, 77 kHz e 200 kHz.
  - ClearVü: CHIRP 455 kHz e CHIRP 800 kHz.
- **Ajustar profundidade, velocidade e ganho.** O ganho pode ser automático ou manual (0–100%), com um controle para o tradicional e outro para o ClearVü.
- **Ver a tela simulada do aparelho**, sozinha ou dividida (tradicional + ClearVü), com cinco paletas de cor.
- **Explorar a cena 3D:**
  - Caiaque de 3,44 m com o transdutor no centro do casco.
  - Feixe com o ângulo real e o valor do ângulo marcado.
  - Pegada do feixe no fundo.
  - Câmeras subaquática, lateral, de popa e de superfície.
- **Comparar a área coberta** por cada frequência, em escala, na vista de cima do caiaque.
- **Conhecer os peixes simulados:** robalo, corvina, pescada, parati e isca. Cada espécie nada na faixa da coluna d'água em que costuma ficar, e um contador mostra quem está dentro do feixe.
- **Carregar cenários prontos:** galhada na represa, barranco raso, cardume suspenso, mapear pedra, fundo de 30–40 m e procura de cardume.

## Como a simulação funciona

Cada coluna da tela é um *ping*. O simulador lança o feixe a partir do transdutor sobre o mesmo fundo, as mesmas galhadas e os mesmos peixes da cena 3D. Em cada coluna ele calcula:

- **Distância (alcance inclinado)** de cada alvo dentro do feixe. É isso que forma os arcos dos peixes.
- **Força do eco,** conforme o tamanho do peixe, a dureza do fundo (lodo, areia, cascalho, pedra) e o ângulo de incidência.
- **Perda do sinal com a distância.** Frequências altas perdem sinal mais rápido.
- **Sombra acústica** atrás de pedras e galhos no ClearVü.
- **Resolução,** que varia com o tom: CHIRP é mais fino que o tom fixo, e 800 kHz é mais fino que 455 kHz.

| Modo | Feixe | Uso típico |
|---|---|---|
| 77 kHz | 45° (cone) | Procurar cardume em área grande, fundo profundo |
| CHIRP 77 kHz | ≈ 45° (estimado) | Área larga com melhor separação de alvos |
| 200 kHz | 15° (cone) | Detalhe do fundo embaixo do casco |
| CHIRP 200 kHz | ≈ 15° (estimado) | Dia a dia: separar peixe do fundo |
| ClearVü CHIRP 455 kHz | 2,5° × 53° (leque) | Estrutura com bom alcance |
| ClearVü CHIRP 800 kHz | ≈ 1,6° × 33° (estimado) | Máxima nitidez em água rasa (até ~30 m) |

## Rodar localmente

Abra o `index.html` no navegador, ou sirva a pasta:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000
```

## Publicar

**GitHub**

```bash
git init
git add .
git commit -m "Simulador do sonar Striker Vivid 4cv"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/sonar-striker-vivid-4cv.git
git push -u origin main
```

**Vercel:** Add New → Project → importe o repositório. Framework *Other*, sem comando de build, diretório de saída `.`.
**Netlify:** Import from Git, sem comando de build, diretório de publicação `.`.
**GitHub Pages:** Settings → Pages → *Deploy from a branch* → `main` / `(root)`.

## Estrutura

```
index.html            página completa (CSS e JS embutidos)
vendor/three.min.js   three.js r128 (MIT)
vercel.json           cache para os arquivos estáticos (opcional)
```

## Fontes e limitações

- **Opções do aparelho:** opções com o transdutor conectado conforme o menu do Striker Vivid 4cv. O modo simulador do próprio aparelho mostra outra lista (145–230 kHz).
- **Ângulos confirmados:** 77 kHz 45°, 200 kHz 15° e ClearVü 455 kHz 2,5° × 53°, segundo a Garmin, "Beam width values for ClearVü transducers".
- **Ângulos estimados:** os dos modos CHIRP tradicionais e do ClearVü 800 kHz. O ganho automático também é uma aproximação.
- **Alcance:** 1.900 pés no tradicional e 750 pés no ClearVü, segundo especificações de revendas, para água doce. O alcance real depende de salinidade, temperatura, turbidez e velocidade.
- **Uso didático:** a cena 3D e a tela são simulações para explicar as frequências, não capturas do aparelho.
- **Uso independente:** projeto sem vínculo com a Garmin. Garmin, Striker, ClearVü e Vivid são marcas de seus respectivos donos.

## Requisitos

Navegador com WebGL (Chrome, Edge, Firefox, Safari recentes). Em aparelhos com WebGL2, os peixes ganham animação de nado e a superfície das pedras e da madeira ganha relevo. Sem WebGL, a tela do sonar e os diagramas continuam funcionando.

## Licença

three.js é distribuído sob licença MIT. Defina a licença do restante do projeto antes de publicar; por exemplo, MIT.
