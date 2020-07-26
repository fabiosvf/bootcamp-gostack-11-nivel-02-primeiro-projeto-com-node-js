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
- Configurar o parâmetro "scripts" no arquivo "./package.json"
  - Adicionar o código abaixo entre os parâmetros "license" e "dependencies"
```
...
  "scripts": {
    "build": "tsc",
    "dev": "node ./dist/server.js"
  },
...
```
---

## Tecnologias utilizadas

#### Dependências de Projeto
- [express](https://yarnpkg.com/package/express)

#### Dependências de Desenvolvimento
- [@types/express](https://yarnpkg.com/package/@types/express)
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
$ node ./dist/server.js
ou
$ yarn dev
```
