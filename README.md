# Objetivo
Recriar o README do meu perfil do GitHub (repositório joaopcassiano/joaopcassiano) na mesma linguagem visual do meu site de portfólio. O resultado tem que parecer feito à mão por um design developer, não um template de README. Zero emojis em qualquer lugar.

# Quem sou
João Pedro Pereira Cassiano, JP Cassiano, design developer. Estudo Ciência da Computação na UNIFENAS (formatura em 2026), moro em Alfenas, MG, estou entrando no mercado de tecnologia. Slogan: "Design que se move." Frase-chave: "Do layout ao código."

# Linguagem visual (a mesma do site)
- Cores: bg #0B0A0A · surface rgba(255,255,255,.045) · border rgba(255,255,255,.10) · text #EDEAE3 · muted #A39E94 · dim #6E6A63 · accent #FF4D1A (só em detalhes pequenos) · ok #2ED573 (só no ponto de status).
- Fonte: Inter Tight (títulos peso 500, tracking -0.045em, line-height .95).
- Formas: cartões com raio 16, pílulas 999, sem sombras, sem gradientes decorativos. Profundidade só com borda e vidro.
- Assinaturas do site que devem aparecer: o quadrado laranja no ponto final do título, o ponto laranja antes de "Design Developer ©2026", o card de status com ponto verde, a palavra "CASSIANO" gigante e quase invisível ao fundo.

# Limitações do GitHub (respeite)
README não executa JS nem CSS. Então todo o visual vem de SVGs estáticos ou animados (CSS/SMIL dentro do SVG funciona em <img>), referenciados no README por <img>. SVG usado em <img> não carrega fonte nem imagem externa: converta os textos em contornos (paths) com opentype.js usando o Inter Tight (baixe de @fontsource/inter-tight) e embuta a foto em base64. Se não conseguir outlinar, use font-family "Inter Tight", "Helvetica Neue", Arial, sans-serif como fallback e me avise.

# Arquivos a gerar
Crie um script scripts/build-assets.mjs que gera tudo em assets/, para eu poder editar textos e rodar de novo:
1. assets/banner.svg (1200x420): reproduz o hero. Esquerda: "Design Developer ©2026" com ponto laranja, título "Design que" / "se move" (segunda linha em muted, quadrado laranja no fim) e um parágrafo curto em muted. Direita: minha foto (assets/hero.jpg embutida) com máscara em gradiente que dissolve a borda esquerda no fundo. Canto inferior direito: card de status com ponto verde ("Disponível para novos projetos", "Alfenas, MG"). Ao fundo: "CASSIANO" gigante em branco a 5%. Uma única animação de entrada (as duas linhas do título subindo de uma máscara, 0,9s, expo.out) e o ponto verde pulsando devagar. Respeitar prefers-reduced-motion.
2. assets/o-que-faco.svg: três cartões lado a lado, UI/UX Design (interfaces e design systems), Front-end (HTML, CSS, JavaScript e TypeScript), Motion e interação (animações com GSAP). Sem ícones coloridos.
3. assets/projeto-cuidado-mais.svg, assets/projeto-controle-de-caixa.svg e assets/projeto-portfolio.svg: cartões de projeto no mesmo estilo, com nome, uma frase, chips da stack e um pequeno rótulo (TCC, Desktop, Site). Textos abaixo.
4. assets/stack.svg: chips em pílula, monocromáticos (borda + texto muted), nada de logos coloridos. Agrupados em Design (Figma), Front-end (HTML, CSS, JavaScript, TypeScript, React, GSAP), Mobile e dados (React Native, Expo, Firebase, C#, SQL Database, Python, Java).
5. assets/contato.svg: pílulas "Portfólio", "LinkedIn", "E-mail", "Instagram" no estilo do botão do site (pílula clara com círculo escuro e seta). Como SVG não tem links, no README cada uma vira um <a> separado com um SVG por pílula (assets/contato-portfolio.svg etc.).
6. .github/workflows/snake.yml: a cobrinha com Platane/snk/svg-only@v3, saída dist/snake-orange.svg com color_snake=#ff4d1a, color_dots=#161514,#4a2a1f,#8f3a1d,#d9461a,#ff4d1a e color_dot_border=#0b0a0a, publicada na branch output via crazy-max/ghaction-github-pages, com cron a cada 12h e workflow_dispatch. Use github_user_name: ${{ github.repository_owner }}.
7. README.md montando tudo, centralizado onde fizer sentido.

# Estrutura do README.md
Banner, linha de status em texto simples, "O que eu faço", "Projetos", "Stack", "Contribuições" (com a cobrinha laranja), "Em números" (cartão de linguagens do github-readme-stats com o tema do site: bg_color=0B0A0A, title_color=FF4D1A, text_color=A39E94, border_color=2A2927) e fechamento com "Do layout ao código." grande e os links de contato. Títulos de seção em texto simples, frase normal, sem emoji e sem ícones decorativos.

# Textos (use exatamente, em português do Brasil)
- Parágrafo do banner: "Sou JP Cassiano, design developer. Desenho sites e produtos digitais e também escrevo o código, então o layout que você aprova é o mesmo que vai para o ar."
- Cuidado+ (TCC): "App mobile para cuidadores acompanharem a saúde de um familiar idoso, com medicamentos, consultas, atividades, relatórios em PDF e assistente de IA." Chips: React Native, Expo, Firebase. Link: https://joaopcassiano.github.io/cuidado-mais-web/
- Controle de caixa: "App desktop em C# com SQL Database para empreendedores controlarem produtos e gerarem relatórios em PDF por período." Chips: C#, SQL Database.
- Portfólio: "Meu site, com abertura em zoom no scroll e animações em GSAP." Chips: HTML, CSS, JavaScript, GSAP. Link: LINK-DO-SEU-SITE
- E-mail: dev.jpcassiano@gmail.com · Instagram: https://instagram.com/_9joaopedro · LinkedIn: LINK-DO-SEU-LINKEDIN
- Não invente nomes de repositório, datas, números ou links. Onde faltar, deixe um TODO claro no código e liste os TODOs no fim.

# Regras de qualidade
- Nenhum emoji, nenhum símbolo decorativo, nenhum badge colorido do shields.io, nenhum banner pronto de serviço externo (capsule-render etc.).
- Cada SVG com no máximo ~400 KB (a foto comprimida) e com <title> e <desc> para acessibilidade; todo <img> do README com alt descritivo.
- Tem que ficar bom no tema claro e no escuro do GitHub: cada SVG leva o próprio fundo escuro, então o README não depende do tema do visitante.
- O laranja só aparece nos pontos pequenos descritos. Se estiver exagerando, tire.
- No fim, rode uma verificação que falhe se encontrar qualquer emoji (regex Unicode) nos arquivos gerados, mostre o tamanho de cada arquivo e me diga como publicar (commit, push, rodar o workflow manualmente na aba Actions).

# Cobrinha com commits privados
Me lembre, no fim, de ativar "Include private contributions on my profile" em Settings → Public profile e "Read and write permissions" em Settings → Actions → General, senão a cobrinha só mostra o que é público.
