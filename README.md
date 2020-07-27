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
### Instalando bibliotecas e editando configurações
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
```
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
- [Padrões de projeto com ESLint, Prettier e EditorConfig](docs/Padr%c3%b5es+de+projeto+com+ESLint%2c+Prettier+e+EditorConfig.pdf)
#### Ferramentas para padronização de código
- [EditorConfig](docs/EditorConfig.pdf)
- [ESLint](docs/ESLint.pdf)
- [Prettier](docs/Prettier.pdf)

---

## Tecnologias utilizadas

#### Dependências de Projeto
- [express](https://yarnpkg.com/package/express)

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
$ ts-node-dev src/server.ts
ou
$ yarn dev:server
```
