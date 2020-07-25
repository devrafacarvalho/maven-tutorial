#Maven

## O que é o Maven?

O Maven é uma ferramenta desenvolvida pela Apache, ela serve para gerenciar as dependências e automatizar seus builds.

Principais funções notadas:
- Gerênciar dependências
- Automatizar builds
- Execução de testes
- Geração de relatórios de teste
- Limpeza do projeto

## Instalando Maven

Para instalar o Maven, basta fazer o download no site e descompactá-lo na sua pasta de preferência.
Após isso adicione-o em suas varíavels do sistema.

## Testando instalação do Maven

Executar no cmd:

```
maven --version
```

## Gerando projeto utilizando maven

Executar no cmd:

```
mvn archetype:generate -DartifactId=produtos -DgroupId=br.com.alura.maven -DinteractiveMode=false -DarchetypeArtfactId=maven-archetype-quickstart
```

**mvn**: Chama o maven, por trás dos panos chama utilizando a variável de ambiente.
**archetype:generete**: utilizado para geração de um novo projeto.
**-DartifactId**: nome do projeto.
**-DgroupId**: pacote inteiro onde ficará o projeto.
**-DinteractiveMode**: se será utilizado o movo interativo do Maven ou não, caso não, ele aceitará as configurações da forma que estão sendo passadas e não irá perguntar mais nada.
**-DarchetypeArtfactId**: aqui você diz qual padrão de projeto será utilizado para a geração do seu. e.x: projetos Web, projetos Spring, etc.
Neste caso foi gerado baseado em um projeto quickstart.

## Compilar utilizando Maven

Você precisa estar com o cmd dentro da pasta do projeto e executar o comando:

```
mvn compile
```

## Executar classe de teste

Você precisa estar com o cmd dentro da pasta do projeto e executar o comando:

```
mvn test
```

## Limpar o projeto

O comando clean do maven retira todos os arquivos compilados ou desnecessários deixando apenas o código-fonte, o arquivo pom.xml e os que são realmente necessários.

```
mvn clean
```

## Gerar relatórios de teste

Você utiliza um plugin para geração dos retalórios de teste. Neste caso o nome do plugin é Surefire Report.

```
mvn surefire-report:report
```

## Empacotar em um arquivo .jar

Para gerar um arquivo .jar do projeto, execute o seguinte comando no cmd.

```
mvn package
```

## Repositório local e remoto

Para execução de um comando Maven offline, acrescente o parâmetro **-o**.

```
mvn -o test
```

Dessa forma o Maven executa sem acessar a internet para procurar versões atualizadas das aplicações necessárias para execução do comando. Esse comando deve ser utilizado com cuidado pois é necessário que já existam em sua máquina as ferramentas necessárias para execução do comando.

Maven busca em seu repositório central na internet (Repositório Remoto).
Maven também guarda as libs necessárias em seu repositório local no diretório .m2/repository (Repositório Local).

A vantagem de se manter um repositório local é que é possível realizar um cache entre vários projetos que utilizam o Maven. Dessa forma, tudo que já estiver salvo no repositório local é utilizado e compartilhado, não sendo necessário realizar novos downloads.

Vale lembrar que o repositório local fica disponível na pasta do usuário, e por esse motivo não estará disponível para diferentes usuários de um mesmo computador.

## As fases do Maven

1. Validação: verificamos se projeto possui todas as informações necessárias

2. Compilação: compilar os conteúdos

3. Teste: realizar testes diferentes no projeto

4. Pacote: geração de um pacote do projeto

5. Teste de integração: realizar testes de integração

6. Verificação: checagem do pacote gerado

7. Instalação: realizar a instalação do pacote no repositório local

8. Implantação: realizar a implantação no ambiente adequado

Quando tratamos do Maven, a execução de um passo depende da execução dos passos anteriores, a não ser que sejam definidos parâmetros, e.g: -DskipTests=true.

## Incluindo plugins
