# Portfólio Pessoal – Felipe Messias

**Aluno:** Felipe Messias
**Atividade:** Agenda 15 – Desenvolvimento de Sistemas I (ETEC)

🔗 **Site publicado:** https://ofelipemessias.github.io/portfolio/

## Descrição do portfólio

Site pessoal para apresentar quem sou, as tecnologias que uso, meus projetos e formas de contato.
Ele foi construído a partir do projeto desenvolvido em aula e evoluído com:

- meus dados, minha foto, meus projetos reais e meus contatos;
- a minha **identidade visual** (cores, fonte Poppins, logotipo e favicon), aplicada em todo o site;
- capas próprias para os projetos e slides do carousel criados no mesmo estilo;
- animações e uma versão otimizada para celular.

## Tecnologias utilizadas

- **HTML5**: estrutura da página, incluindo a tag `<picture>` para imagens responsivas
- **CSS3**: personalização, variáveis de cor, transições, animações e media queries
- **Bootstrap 5.3**: menu (navbar), carousel, grid responsivo, cards, botões e Scrollspy
- **JavaScript**: animação de entrada ao rolar, botão "voltar ao topo" e fechamento do menu no celular
- **Google Fonts (Poppins)** e **Devicon**: fonte e ícones das tecnologias
- **Python (Pillow)**: geração das capas e dos slides com a identidade visual
- **GitHub Pages**: publicação do site

## Como o projeto funciona

O site é uma página única (`index.html`) com as imagens na pasta `imagens/`:

1. **Menu de navegação** fixo no topo (`sticky-top`), em azul-marinho, com o logotipo, os links Perfil e
   Projetos e o botão **Fale comigo**. Cada link aponta para o `id` de uma seção. O **Scrollspy** do Bootstrap
   destaca a seção que está na tela com um sublinhado verde. No celular, o menu vira um botão "hambúrguer".
2. **Carousel** com três slides da minha identidade visual e transição suave (`carousel-fade`).
3. **Perfil**: foto, apresentação, cards com localização, área de interesse, formação e objetivo, além das
   tecnologias que utilizo.
4. **Projetos**: três cards com capas próprias e um link para cada projeto.
5. **Contato**: botões para e-mail, GitHub e LinkedIn.
6. **Rodapé**.

### Identidade visual

As cores ficam em variáveis CSS, reaproveitadas no menu, nos botões e no rodapé:

```css
:root {
    --marinho: #0A2540;
    --royal: #2563EB;
    --verde: #22C55E;
}
```

As capas dos projetos e os slides seguem o mesmo padrão: fundo azul-marinho com brilho azul, título em
Poppins terminado pelo ponto verde (assinatura da marca) e a linha de "nós conectados" do logotipo.

## Recurso novo adicionado

1. **Animação de entrada ao rolar a página:** o perfil, os títulos, os cards de projetos e o card de contato
   começam invisíveis e surgem subindo suavemente quando aparecem na tela.
2. **Efeito hover nos cards de projetos:** ao passar o mouse, o card sobe e ganha uma sombra azul.
3. **Botão "voltar ao topo"**, que aparece depois de rolar a página.
4. **Versão otimizada para celular:** slides próprios no formato quadrado, espaçamento menor entre as seções,
   foto de perfil menor e menu que fecha sozinho ao tocar em um link.

## Como o recurso foi implementado

**Hover nos cards (CSS):** os cards da seção Projetos receberam uma `transition`. No `:hover`, o
`transform: translateY(-10px)` faz o card subir e o `box-shadow` adiciona a sombra.

```css
#projetos .card { transition: transform 0.3s, box-shadow 0.3s; }
#projetos .card:hover {
    transform: translateY(-10px);
    box-shadow: 0 15px 30px rgba(13, 110, 253, 0.25) !important;
}
```

**Animação ao rolar (CSS + JavaScript):**

- No **HTML**, os blocos que devem animar receberam a classe `animar`.
- No **CSS**, `.animar` deixa o elemento invisível (`opacity: 0`) e 40px mais baixo. A classe `.visivel` traz
  o elemento de volta, e a `transition` faz o movimento.

```css
.animar { opacity: 0; transform: translateY(40px); transition: opacity 0.8s ease, transform 0.8s ease; }
.animar.visivel { opacity: 1; transform: translateY(0); }
```

- No **JavaScript**, um `IntersectionObserver` vigia todos os elementos `.animar`. Quando um deles aparece na tela
  (pelo menos 15% visível), o script adiciona a classe `visivel` e para de vigiar aquele elemento, para animar só uma vez.

```js
const observador = new IntersectionObserver(function (entradas) {
    entradas.forEach(function (entrada) {
        if (entrada.isIntersecting) {
            entrada.target.classList.add("visivel");
            observador.unobserve(entrada.target);
        }
    });
}, { threshold: 0.15 });

document.querySelectorAll(".animar").forEach(function (elemento) {
    observador.observe(elemento);
});
```

**Botão voltar ao topo:** um evento `scroll` verifica se a página foi rolada mais de 400px e, nesse caso,
adiciona a classe `mostrar`, que deixa o botão visível.

**Versão para celular:**

- Cada slide usa a tag `<picture>`. Em telas de até 767px, o navegador carrega a versão quadrada; nas maiores,
  a versão larga. As setas do carousel ficam escondidas no celular (`d-none d-md-flex`), onde os slides
  passam com o dedo.

```html
<picture>
    <source media="(max-width: 767px)" srcset="imagens/slide1-mobile.png">
    <img src="imagens/slide1.png" class="d-block w-100" alt="Olá, eu sou Felipe Messias">
</picture>
```

- Uma media query `@media (max-width: 767px)` reduz o espaçamento das seções e o tamanho da foto, e deixa os
  links do menu maiores para o toque.
- Um script fecha o menu aberto depois que um link é tocado, usando `bootstrap.Collapse`.

## Estrutura de arquivos

```
portfolio/
├── index.html
├── README.md
└── imagens/
    ├── felipe.jpg                 # foto do perfil
    ├── logo.png, favicon.png      # logotipo e ícone da aba
    ├── slide1.png ... slide3.png  # slides do carousel (computador)
    ├── slide1-mobile.png ...      # slides do carousel (celular)
    └── este-portfolio.png, sites-favoritos.png, brand-kit-capa.png  # capas dos projetos
```

## Como executar

- Online: https://ofelipemessias.github.io/portfolio/
- No computador: baixe o repositório e abra o `index.html` no navegador.
