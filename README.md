####  Bootcamp - GoStack 11
# 🚀 Nível 02 - Primeiro projeto com Node.js

## Sobre

- Esta API contém o back-end do Projeto GoBarber.
- Neste projeto será utilizado Node.js com TypeScript, além de ferramentas como ts-node-dev, ESLint, Prettier e EditorConfig.

---

## Roteiro

- Nesta seção será descrito o roteiro com todos os passos para criação do projeto em Node.js com TypeScript

### Criando o projeto
- Criar uma pasta
- Acessar a pasta em modo terminal
- Criar o arquivo "package.json" com a configuração padrão
```
$ yarn init -y
```
- Abrir a pasta do projeto no Visual Studio Code
```
$ code .
```
### Instalando bibliotecas e editando configurações iniciais
- Instalar a biblioteca "express"
  - Responsável por fornecer recursos em formato de serviço para aplicações web e dispositivos móveis, utilizando como comunicação o protocolo HTTP em conjunto com o padrão RESTFULL
```
$ yarn add express
```
- Instalar a biblioteca "typescript" como dependência de desenvolvimento
  - Responsável por fornecer recursos de definição de tipos que auxiliam o desenvolvimento em JavaScript
```
$ yarn add typescript -D
```
- Criar o arquivo "tsconfig.json"
  - Responsável por armazenar todas as configurações de como o TypeScript irá se comportor dentro do projeto
```
$ yarn tsc --init
```
- Criar a estrutura padrão para teste
  - Criar a pasta "src" na raiz do projeto
  - Criar o arquivo "server.ts" dentro da pasta recém criada
```js
import express, { request, response } from 'express';

const app = express();

app.get('/', (request, response) => {
  return response.json({ message: 'Hello World' });
});

app.listen(3333, () => {
  console.log('🚀 Server started on port 3333!')
});
```
- Configurar as propriedades "outDir" e "rootDir"
  - "outDir" responsável por armazenar o build da aplicação, ou seja, converter os arquivo (.ts) em arquivos (.js) compatíveis.
    - Por convenção iremos definir o valor como "./dist"
  - "rootDir" responsável pro armazenar os arquivos TypeScript (.ts) desenvolvidos no projeto.
    - Por convenção iremos definir o valor como "./src"
```
...
    "outDir": "./dist",                       /* Redirect output structure to the directory. */
    "rootDir": "./src",                       /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
...
```
- Instalar a biblioteca "@types/express" como dependência de desenvolvimento
  - Responsável por disponibilizar a declaração de tipos da biblioteca "express"
```
$ yarn add @types/express -D
```
- Instalar a biblioteca "ts-node-dev" como dependência de desenvolvimento
  - Responsável por monitor alterações no código e atualizar o serviço sem a necessidade de reiniciar o serviço manualmente
  - É uma alternativa para o "nodemon", "babel", "webpack", "sucrase" e "tsc" em modo watch
  - É extremamente rápido e proporciona uma experiência bacana de desenvolvimento
```
$ yarn add ts-node-dev -D

```
- Configurar o parâmetro "scripts" no arquivo "./package.json"
  - Adicionar o código abaixo entre os parâmetros "license" e "dependencies"
  - "transpile-only" serve para informar ao ts para apenas converter, e não validar se o código está correto. Isso aumenta a performance
  - "ignore-watch" serve para ignorar alterações que ocorrerem na pasta informada como parâmetro, no nosso caso, "node_modules"
```json
...
  "scripts": {
    "build": "tsc",
    "dev:server": "ts-node-dev --transpile-only --ignore-watch node_modules src/server.ts"
  },
...
```
---

## Padrões de Projeto

#### Introdução
- [Padrões de projeto com ESLint, Prettier e EditorConfig](docs/Padrões%20de%20projeto%20com%20ESLint%2C%20Prettier%20e%20EditorConfig.pdf)
#### Ferramentas para padronização de código
- [EditorConfig](docs/EditorConfig.pdf)
- [ESLint](docs/ESLint.pdf)
- [Prettier](docs/Prettier.pdf)

---

## Debug no VS Code

#### Configurando o Debug no Visual Studio Code
- Abrir a tela de configuração do Debug
  - Acessar o menu _View > Run_ ou pressioner _Ctrl + Shift + D_
  - Clicar em _create a launch.json file_ para criar o arquivo "launch.json"
  - Caso solicite mais alguma informação, selecione "Node.js"
```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "protocol": "inspector",
      "restart": true,
      "name": "Debug",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "outFiles": [
        "${workspaceFolder}/**/*.js"
      ]
    }
  ]
}
```
- Além disso, será necessário alterar o script "dev:server" no arquivo de configuração "package.json"
```json
...
"scripts": {
    "build": "tsc",
    "dev:server": "ts-node-dev --inspect --transpile-only --ignore-watch node_modules src/server.ts"
  },
...
```
#### Debugando um código
- Inicie o servidor
```
$ yarn dev:server
```
- Clique no Menu _Run > Starting Debug_ ou pressione _F5_
- Coloque **break points** na parte do código que deseja inspecionar. Para isso clique na lateral esquerda do código sobre a número da linha, e um ponto vermelho irá aparecer.
- Efetue a requisição para inspecionar a parte do código desejada

---

## Construindo Aplicação

#### Cadastro de Agendamentos
- Dividir o arquivo de rotas de acordo com cada entidade da aplicação
  - O arquivo principal das rotas será `./src/routes/index.ts`
  - Os demais arquivos seguirão um formato padrão adotando o nome da entidade + o sufixo routes
    - Em nosso caso iniciaremos com a criação do arquivo `./src/routes/appointments.routes.ts`
- Instalar a biblioteca "uuidv4"
  - Essa biblioteca será responsável por gerar um ID único para o cadastro de nossas entidades
```
$ yarn add uuidv4
```

#### Validando a data
- Instalar a biblioteca "date-fns"
  - Essa biblioteca será responsável por trabalhar com datas e horários dentro do nosso serviço
```
$ yarn add date-fns
```
- Implementar validação para a data do agendamento
  - A validação será implementada no arquivo `./src/routes/appointments.routes.ts`

#### Model de Agendamento
- Criar Models em uma área exclusiva para facilitar a reutilização desses modelos
  - Os Models são os modelos das entidades criados como `interface`
  - Essas estruturas serão criadas na pasta `./src/models`
  - Por convenção, adotamos a inicial do model em maiúscula e no singular, no nosso caso, `./src/models/Appointment.ts`

#### Criando repositórios
- Aplicar o conceito de `repositórios`
  - O repositório nada mais é do que uma conexão entre a persistência dos dados no banco de dados e a nossa rota
  - `Persistência <-> Repositório <-> Rota`
  - Em geral nós temos um Repositório por Model, no qual é responsável por criar, armazenar, ler, deletar e editar os dados
  - Essas estruturas serão criadas na pasta `./src/repositories`
  - Por convenção, adotamos o nome do model no plural com a inicial maiúscula + o sufixo `Repository`, no nosso caso, `./src/repositories/AppointmentsRepository.ts`

#### Listando Agendamentos
- Continuar o refatoramento das rotas
  - Seguindo o conceito de `SoC (Separation of Concerns / Separação de preocupações)`, a rota não deve ter outras responsabilidades a não ser a de receber as requisições e direcionar para outros módulos que possuem responsabilidades específicas. Desta forma, o código fica limpo e fácil entender e de dar manutenção.
  - Nesta tarefa foi criado uma rota para obter todos os repositórios. Os arquivos editados foram:
    - `./src/repositories/AppointmentsRepository.ts`
    - `./src/routes/appointments.routes.ts`

#### Trabalhando com dados
- Aplicar o conceito de `DTO - Data Transfer Object`
  - O conceito de DTO permite que organizemos e consolidemos as propriedades em um único objeto afim de serem utilizados na passagem de parâmetros entre os métodos.
  - Esse conceito deve substituir a passagem de parametros avulsos
  - Seguem os arquivos editados nesta tarefa:
    - `./src/repositories/AppointmentsRepository.ts`
    - `./src/routes/appointments.routes.ts`
- Tipar em forma de objeto, os parametros do construtor do Model
  - Para isso utilizaremos a função `Omit` que permite, além de informar o modelo de tipagem utilizado nos parâmetros de entrada, também em caracter de exceção, quais parâmetros devem ser ignorados na assinatura do construtor, por já possuírem algum tratamento dentro do próprio construtor. No nosso exemplo, o campo `id`.
  - Segue o arquivo editado nesta tarefa:
    - `./src/models/Appointment.ts`

#### Services & SOLID
- Aplicar o conceito de `Services`
  - O conceito de Services permite armazenar toda a regra de negócio da nossa aplicação
  - Cada serviço deve ter apenas uma única funcionalidade, obedecendo dois princípios importantes `Single Responsability Principle (SOLID)` e `DRY - Don't Repeat Yourself`
  - Em resumo, um service é responsável pelo:
    - Recebimento das informações
    - Tratamento de erros/excessões
    - Acesso ao repositório
  - Essas estruturas serão criadas na pasta `./src/services`
  - Por convenção, adotamos o nome do service de acordo com sua regra de negócio. O nome deve estar no singular com a inicial maiúscula + o sufixo `Service`, no nosso caso, `./src/services/CreateAppointmentService.ts`
- Aplicar o conceito de `Dependency Inversion Principle (SOLID)`
  - Em resumo, este conceito significa compartilharmos o mesmo repositório em mais de um Service
  - Para que isso aconteça, precisaremos passar o repositório como parâmetro do construtor do Service
  - Seguem os arquivos editados nesta tarefa:
    - `./src/repositories/AppointmentsRepository.ts`
    - `./src/services/CreateAppointmentService.ts`
- Documentos adicionais
  - [Repository, service e patterns](docs/Repository%2C%20service%20e%20patterns.pdf)
  - [Princípios do SOLID](docs/Princ%C3%ADpios%20do%20SOLID.pdf)

---

## Tecnologias utilizadas

#### Dependências de Projeto
- [date-fns](https://yarnpkg.com/package/date-fns)
- [express](https://yarnpkg.com/package/express)
- [uuidv4](https://yarnpkg.com/package/uuidv4)

#### Dependências de Desenvolvimento
- [@types/express](https://yarnpkg.com/package/@types/express)
- [@typescript-eslint/eslint-plugin](https://yarnpkg.com/package/@typescript-eslint/eslint-plugin)
- [@typescript-eslint/parser](https://yarnpkg.com/package/@typescript-eslint/parser)
- [eslint](https://yarnpkg.com/package/eslint)
- [eslint-config-airbnb-base](https://yarnpkg.com/package/eslint-config-airbnb-base)
- [eslint-config-prettier](https://yarnpkg.com/package/eslint-config-prettier)
- [eslint-import-resolver-typescript](https://yarnpkg.com/package/eslint-import-resolver-typescript)
- [eslint-plugin-import](https://yarnpkg.com/package/eslint-plugin-import)
- [eslint-plugin-prettier](https://yarnpkg.com/package/eslint-plugin-prettier)
- [prettier](https://yarnpkg.com/package/prettier)
- [ts-node-dev](https://yarnpkg.com/package/ts-node-dev)
- [typescript](https://yarnpkg.com/package/typescript)

---

## Como executar
- Crie uma pasta para o projeto
- Acesse a pasta
- Faça o clone do projeto
```
$ git clone https://github.com/fabiosvf/bootcamp-gostack-11-nivel-02-primeiro-projeto-com-node-js.git .
```
- Atualize as bibliotecas
```
$ yarn
```
- Converta TypeScript em JavaScript
```
$ yarn tsc
ou
$ yarn build
```
- Inicie o serviço
```
$ ts-node-dev --inspect --transpile-only --ignore-watch node_modules src/server.ts
ou
$ yarn dev:server
```
