<h4 align="center">
  <img src=".github/nest.svg" />

  <p>Fundamentos do NestJS + Clean Code</p>
</h4>

Aplicação para aprender os fundamentos do framework NestJS.

O NestJS traz muitas opiniões e convenções sobre como construir as coisas dentro dele. Ele é ótimo quando você precisa de produtividade e não tem ninguém para guiar as escolhas técnicas. O NestJS permite que você estruture as pastas do projeto da maneira que quiser, mas traz preferências e recomendações para ferramentas como validação, mensageria, GraphQL, WebSocket e ORM.

> ⚠️ Aplicação com finalidade de desenvolver minhas habilidades com NestJS

## ✨ Tecnologias relevantes

- [NestJS](https://docs.nestjs.com): Nest (NestJS) é uma estrutura para a construção de aplicativos Node.js do lado do servidor eficientes e escalonáveis.
- [Zod](https://zod.dev): Zod é uma biblioteca de validação de dados para TypeScript.
- [Passport](https://www.passportjs.org/): Passport é uma biblioteca de autenticação de usuários do lado do servidor.
- [Passport JWT](https://www.passportjs.org/packages/passport-jwt/): Uma estratégia do Passport para autenticação com um JSON Web Token, este módulo permite autenticar endpoints usando um token web JSON.
- [Prisma](https://www.prisma.io/): Prisma é uma biblioteca de persistência de banco de dados para Node.js

## 🧑‍🏭 Executando a aplicação

Levando em conta que o projeto já foi clonado e está com todas as dependências instaladas usando seu principal gerenciador de pacotes:

```bash
$ pnpm install
```

Adicione as variáveis de ambiente copiando o arquivo `.env.example` e renomeando para `.env`:

```properties
# Database
DATABASE_URL="postgresql://postgres:docker@localhost:5432/nest-fundamentals?schema=public"

# Auth
JWT_PRIVATE_KEY=""
JWT_PUBLIC_KEY=""

# Application
PORT=""
```

A estratégia de autenticação usada é JWT com algorítimo RSA-256. Logo você deve gerar as chaves pública e privada do algoritmo e convertê-las para Base64.

```bash
$ openssl genrsa -out private.pem 2048
$ openssl rsa -in private.pem -pubout -out public.pem

$ base64 private.pem
$ base64 public.pem
```

Usando o docker-compose inicie os serviços necessários para executar a aplicação com:

```bash
$ docker-compose up -d
```

Não esqueça de rodar as migrações:

```bash
$ pnpm prisma migrate dev
```

Após isso basta iniciar a aplicação (desenvolvimento):

```bash
$ pnpm run start:dev
```

## 🦉 Requisições

Para testar as requisições da aplicação estou usando a extensão do VSCode chamada [Rest Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) e com ela criei um arquivo chamado `client.http` na raiz do projeto onde estão listadas todas as rotas da aplicação.

## 📃 Anotações importantes

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

**Docker compose**

O docker compose é essencial quando seu projeto depende de vários serviços como banco de dados, Kafka ou até ferramentas de CDN como Minio.

**O que são Pipes?**

Um pipe é uma classe anotada com o `@Injectable()` decorador, que implementa a `PipeTransform` interface.

Pipes têm dois casos de uso típicos:

- transformação : transforma os dados de entrada na forma desejada (por exemplo, de string para inteiro)
- validação : avalia os dados de entrada e, se válidos, simplesmente passa-os inalterados; caso contrário, lance uma exceção

Em ambos os casos, os pipes operam sendo argumentos processados ​​por um manipulador de rotas do controlador. Nest interpõe um pipe logo antes de um método ser invocado, e o pipe recebe os argumentos destinados ao método e opera sobre eles. Qualquer operação de transformação ou validação ocorre nesse momento, após o qual o manipulador de rota é invocado com quaisquer argumentos (potencialmente) transformados.

**Autenticação JWT com algoritmo RSA-256**

A autenticação JWT (JSON Web Token) com algoritmo RSA-256 é um método de autenticação que utiliza chaves assimétricas para garantir a autenticidade e integridade dos tokens gerados.

A diferença entre a autenticação JWT com algoritmo RSA-256 e outras formas de autenticação reside no uso de chaves assimétricas. Em vez de usar uma chave compartilhada entre o emissor e o receptor, como na autenticação JWT com algoritmo HMAC, a autenticação JWT com algoritmo RSA-256 utiliza um par de chaves: uma chave privada para assinar (criptografar) o token e uma chave pública para verificar a assinatura.

A principal vantagem da autenticação JWT com algoritmo RSA-256 é a capacidade de verificar a autenticidade do token sem a necessidade de compartilhar uma chave secreta entre o emissor e o receptor. Isso torna mais seguro e escalável em cenários onde há múltiplos emissores e receptores envolvidos.

No entanto, a autenticação JWT com algoritmo RSA-256 também tem algumas desvantagens. É mais computacionalmente intensiva do que a autenticação JWT com algoritmo HMAC, devido ao uso de criptografia assimétrica. Além disso, a gestão das chaves privadas e públicas pode ser mais complexa em comparação com o uso de uma única chave compartilhada.

**O que é o SWC? Qual a diferença entre o SWC e o ESBuild?**

SWC é uma plataforma extensível baseada em Rust e pode ser usado tanto para compilação quanto para agrupamento. Para compilação, são necessários arquivos JavaScript/TypeScript usando recursos JavaScript modernos e gera código válido que é compatível com todos os principais navegadores.

O ESBuild é um empacotador e minificador JavaScript 10-100x mais rápido do que as ferramentas existentes, escrito em Go.

Um detalhe importante é que o SWC para os testes E2E se sai muito melhor nos casos desta aplicação, pois ele entende Decorators e o ESBuild não, logo ele é mais rápido. Sendo assim usar o ESBuild, que é o padrão do Vite e do Vitest, acaba deixando os testes um pouco mais lentos.

**Sobre testes E2E**

Quando trabalhamos com testes de ponta a ponta é necessário que eles estejam o mais próximo possível do ambiente real da aplicação, ou seja, quanto menos mocks ou comportamentos fictícios forem adicionados no código para pular algo, melhor, pois vai evitar falsos positivos ou falos negativos.

Quando vamos testar uma rota é importante que estejamos fazendo o fluxo completo, desde bater no banco de dados com a informação quanto usando os serviços que o usuário usaria para acessar a rota.

Uma das coisas que é importante é sempre ter um ambiente isolado para testes, para que não haja interações entre os testes.