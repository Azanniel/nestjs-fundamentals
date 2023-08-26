# NestJS Fundamentos

Aplicação para aprender os fundamentos do framework NestJS.

O NestJS traz muitas opiniões e convenções sobre como construir as coisas dentro dele. Ele é ótimo quando você precisa de produtividade e não tem ninguém para guiar as escolhas técnicas. O NestJS permite que você estruture as pastas do projeto da maneira que quiser, mas traz preferências e recomendações para ferramentas como validação, mensageria, GraphQL, WebSocket e ORM.

## Anotações importantes

**1. Qual a diferença entre o NestJS e o Express/Fastify?**

Ele é um framework (construído encima do Express) muito mais opinado para desenvolvimento de APIs. Logo, ele traz muita opinião em como você vai fazer as coisas usando o framework.
Nas suas documentos, inclusive, existem muitas receitas caso você vá utilizar ferramentas como GraphQL ou Banco de dados ou até mensageria assíncrona.

**2. Quando usar o NestJS?**

Imagina que você está desenvolvendo uma aplicação e que dentro do time não existe uma pessoa que vai guiá-los nas escolhas técnicas ou que vai conseguir tomar todas as melhores decisões e você e o time precisam de produtividade, então o NestJS é uma boa escolha. Tudo porque ele traz opinião própria e você perde menos tempo pensando em qual biblioteca você deve usar para solucionar alguns problemas simples aos quais ele traz algumas receitas de como resolver.

**3. Como funciona a estrutura base no NestJS?**

O NestJs tem uma opinião muito grande nos tipos de arquivos que criamos em nossa aplicação.

- Controller - Arquivo que controla as rotas do projeto.
- Module - É um arquivo que reúne todas as coisas em um módulo só.
- Service - É um arquivo que executa tudo que é necessário para dar resposta ao seu controlador.

Características do Nest:
- Uso de decorators que são funções que adicionam comportamento em algo.
- Inversão de dependência e Injeção de dependência.