# Portfólio Pessoal – Felipe Messias

**Aluno:** Felipe Messias
**Atividade:** Agenda 15 – Desenvolvimento de Sistemas I (ETEC)

🔗 **Site publicado:** https://ofelipemessias.github.io/portfolio/

## Descrição do portfólio

Site pessoal para apresentar quem sou, as tecnologias que uso, meus projetos e formas de contato.
Ele foi construído a partir do projeto desenvolvido em aula e personalizado com meus dados, minha foto,
meus projetos reais e novos recursos de animação.

## Tecnologias utilizadas

- **HTML5**: estrutura da página
- **CSS3**: personalização, transições e animações
- **Bootstrap 5.3**: menu (navbar), carousel, grid responsivo, cards e botões
- **Devicon**: ícones das tecnologias
- **JavaScript**: animação de entrada ao rolar e botão "voltar ao topo"
- **GitHub Pages**: publicação do site

## Como o projeto funciona

O site é uma página única (`index.html`) com as imagens na pasta `imagens/`. A página tem:

1. **Menu de navegação** fixo no topo (`sticky-top`). Cada link aponta para o `id` de uma seção
   (`#perfil`, `#projetos`, `#contato`), e no celular ele vira um botão "hambúrguer".
2. **Carousel** com três imagens de destaque e transição suave (`carousel-fade`).
3. **Perfil**: foto, apresentação, cards com localização, área de interesse, formação e objetivo,
   além das tecnologias que utilizo.
4. **Projetos**: três cards com os meus projetos e um link para cada repositório.
5. **Contato**: botões para e-mail, GitHub e LinkedIn.
6. **Rodapé**.

## Recurso novo adicionado

1. **Animação de entrada ao rolar a página:** o perfil, os títulos, os cards de projetos e o card de contato
   começam invisíveis e surgem subindo suavemente quando aparecem na tela.
2. **Efeito hover nos cards de projetos:** ao passar o mouse, o card sobe e ganha uma sombra azul.
3. **Bônus: botão "voltar ao topo"**, que aparece depois de rolar a página.

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

## Como executar

- Online: https://ofelipemessias.github.io/portfolio/
- No computador: baixe o repositório e abra o `index.html` no navegador.
