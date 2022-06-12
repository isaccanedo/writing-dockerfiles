# writing-dockerfiles
### Práticas recomendadas para escrever Dockerfiles

Este documento abrange as melhores práticas e métodos recomendados para a criação de imagens eficientes.

O Docker cria imagens automaticamente lendo as instruções de um Dockerfile -- um arquivo de texto que contém todos os comandos, em ordem, necessários para construir uma determinada imagem. Um Dockerfile segue um formato específico e um conjunto de instruções que você pode encontrar na referência do Dockerfile.

Uma imagem do Docker consiste em camadas somente leitura, cada uma representando uma instrução do Dockerfile. As camadas são empilhadas e cada uma é um delta das alterações da camada anterior. Considere este Dockerfile:

```
# syntax=docker/dockerfile:1
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

### Cada instrução cria uma camada
```
- FROM - cria uma camada a partir da imagem ubuntu:18.04 Docker;
- COPY - adiciona arquivos do diretório atual do seu cliente Docker;
- RUN - constrói sua aplicação com make;
- CMD - especifica qual comando executar dentro do contêiner.
```

Ao executar uma imagem e gerar um contêiner, você adiciona uma nova camada gravável (a “camada de contêiner”) sobre as camadas subjacentes. Todas as alterações feitas no contêiner em execução, como gravar novos arquivos, modificar arquivos existentes e excluir arquivos, são gravadas nessa camada de contêiner gravável.

Para saber mais sobre camadas de imagem (e como o Docker cria e armazena imagens), consulte Sobre drivers de armazenamento.
