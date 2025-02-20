# Gerenciamento-de-Configura-o-Jenkins---Projeto-Final


Este repositório contém o Trabalho de Conclusão de Disciplina (TCD) da matéria de Gerenciamento de Configuração, com foco na ferramenta Jenkins. O projeto abrange a instalação, configuração e utilização do Jenkins para automação de pipelines de CI/CD, destacando seus principais recursos e benefícios na gestão de configurações e entrega contínua.



# Projeto Final - Gerenciamento de Configurações - Jenkins @ UFMT/2025

![alt text](Imagens/jenkins.svg)

- **Tecnologia:** [Jenkins](https://www.jenkins.io/)
- **Tecnologias aplicadas:** Java, Groovy, Docker, Kubernetes, Git, GitHub Actions, Pipeline as Code, Shell Script.
- **Integrante:**
  - Elton Marcelino de Lima - Aluno de Especialização DevOps

## 1. Descrição da tecnologia

   Jenkins é uma ferramenta open-source para automação de integração contínua (CI) e entrega contínua (CD). Sua principal função é permitir a automação de builds, testes e deploys de aplicações, facilitando a implementação de DevOps. Jenkins suporta diversos plugins, permitindo integração com ferramentas como Docker, Kubernetes, Git e outras plataformas de CI/CD. Ele resolve problemas relacionados à repetibilidade, automação de processos de desenvolvimento e entrega de software, reduzindo falhas humanas e acelerando a implantação de novas versões de aplicações.

   ### Linguagem utilizada pelo Jenkins
   O Jenkins é desenvolvido na linguagem **Java**, tornando-o multiplataforma e capaz de rodar em diferentes sistemas operacionais, como Windows, Linux e macOS. 
   - Para rodar o Jenkins, é necessário ter uma versão compatível do **Java Runtime Environment (JRE)** ou **Java Development Kit (JDK)** instalada.
   - Ele também utiliza **Groovy** para a definição de pipelines em código, permitindo a criação de pipelines declarativos e em formato de script, o que torna a automação mais flexível.
   - Além disso, pode executar comandos em **Shell Script**, Python, PowerShell e outras linguagens, dependendo das necessidades do projeto e dos plugins instalados.

## 2. Descrição do problema

   Imagine uma equipe de desenvolvimento que trabalha em um grande projeto de software. Os desenvolvedores precisam realizar builds e testes manuais sempre que um novo código é commitado no repositório Git, o que consome tempo e está sujeito a erros humanos. Além disso, o processo de deployment também é feito manualmente, tornando a entrega de novas versões lenta e suscetível a falhas.

   Essa situação causa problemas como:
   - Builds inconsistentes devido a erros manuais.
   - Tempo excessivo gasto em processos repetitivos.
   - Dificuldade em garantir que todas as mudanças foram testadas corretamente.
   - Risco elevado de falhas em produção devido à falta de automação no deployment.

## 3. Solução

   A implementação do Jenkins pode resolver esses problemas por meio da automação do pipeline de CI/CD. Os passos para a solução incluem:

   1. **Instalação do Jenkins**: Configuração do Jenkins em um servidor ou container Docker.
   2. **Integração com o GitHub**: Configuração de webhooks para disparar builds automaticamente após cada commit.
   3. **Definição de um Pipeline as Code**: Utilização de um `Jenkinsfile` para definir o pipeline de build, teste e deploy.
   4. **Execução automatizada de testes**: Configuração de testes automatizados para validar o código antes do deploy.
   5. **Deploy automatizado**: Configuração do Jenkins para fazer o deploy contínuo em um ambiente de homologação ou produção usando Docker/Kubernetes.

   ### Exemplo de `Jenkinsfile`:
   ```groovy
   pipeline {
       agent any
       stages {
           stage('Build') {
               steps {
                   sh 'mvn clean package'
               }
           }
           stage('Test') {
               steps {
                   sh 'mvn test'
               }
           }
           stage('Deploy') {
               steps {
                   sh 'docker build -t myapp:latest .'
                   sh 'docker run -d -p 8080:8080 myapp:latest'
               }
           }
       }
   }
   ```

## Explicação Detalhada do Pipeline

### 1️⃣ pipeline { ... }
O bloco `pipeline {}` define um **pipeline declarativo**, que organiza as tarefas em **stages (etapas)** e permite um fluxo de execução bem definido.

### 2️⃣ agent any
```groovy
agent any
```
- Define em qual **agente** (máquina) o pipeline será executado.
- `any` significa que pode ser executado em qualquer agente disponível no Jenkins.

### 3️⃣ stage('Build') - Construção do Projeto
```groovy
stage('Build') {
    steps {
        sh 'mvn clean package'
    }
}
```
- **Objetivo:** Compilar e construir o código do projeto.
- **Comando executado:** `mvn clean package`
  - `mvn` → Executa o Maven (ferramenta de build para projetos Java).
  - `clean` → Limpa os arquivos de compilação antigos.
  - `package` → Empacota o código em um arquivo `.jar` ou `.war`.

### 4️⃣ stage('Test') - Execução de Testes
```groovy
stage('Test') {
    steps {
        sh 'mvn test'
    }
}
```
- **Objetivo:** Rodar os testes automatizados antes de prosseguir com a implantação.
- **Comando executado:** `mvn test`
  - O Maven executa todos os testes unitários definidos no projeto.
  - Se algum teste falhar, o pipeline para e não continua para a próxima etapa.

### 5️⃣ stage('Deploy') - Implantação da Aplicação
```groovy
stage('Deploy') {
    steps {
        sh 'docker build -t myapp:latest .'
        sh 'docker run -d -p 8080:8080 myapp:latest'
    }
}
```
Essa etapa realiza o deploy da aplicação usando **Docker**.

#### **Passo 1 - Construção da imagem Docker**
```groovy
sh 'docker build -t myapp:latest .'
```
- `docker build` → Cria uma imagem Docker.
- `-t myapp:latest` → Nomeia a imagem como **myapp** com a versão `latest` (mais recente).
- `.` → Usa o `Dockerfile` no diretório atual para construir a imagem.

#### **Passo 2 - Execução do Container**
```groovy
sh 'docker run -d -p 8080:8080 myapp:latest'
```
- `docker run` → Roda um container baseado na imagem criada.
- `-d` → Modo **detached** (em segundo plano).
- `-p 8080:8080` → Mapeia a porta 8080 do container para a porta 8080 do host.
- `myapp:latest` → Usa a imagem recém-criada `myapp:latest`.

## 4. Referências

   - [Documentação Oficial do Jenkins](https://www.jenkins.io/doc/)
   - [Jenkins Pipeline](https://www.jenkins.io/doc/book/pipeline/)
   - [Integração do Jenkins com Docker](https://www.jenkins.io/doc/book/installing/docker/)

