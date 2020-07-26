# Maven

## O que é o Maven

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

Por exemplo:

```
mvn verify irá executar todas as fases anteriores antes de ser executada.
```

## Gerando relatórios e testando projeto utilizando PMD

O arquivo é gerado dentro do diretório target/site.
Consultar documentação para ver todas as formas de uso do PMD.

```
mvn pmd:pmd
```

Para validar o projeto, você pode utilizar o comando:

```
mvn pmd:check
```

Dessa forma você faz a validação padrão do PMD, para personalizá-las utilize a documentação como auxílio.

## pom.xml

É o principal arquivo de configuração de projetos Maven, por ele você pode gerenciar todo o ciclo de vida do projeto.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
        <!-- Versão do arquivo XML-->
	<modelVersion>4.0.0</modelVersion>
        <!-- Caminho inteiro do projeto-->
	<groupId>br.com.rafael.maven</groupId>
        <!-- Nome artifactId-->
	<artifactId>produtos</artifactId>
        <!-- Formato que o projeto será empacotado -->
	<packaging>jar</packaging>
        <!-- Versão do projeto -->
	<version>1.0-SNAPSHOT</version>
        <!-- Nome "bonitinho" para o projeto -->
	<name>produtos</name>
        <!-- Site do seu projeto -->
	<url>http://maven.apache.org</url>
	<dependencies>
                <!-- Dependência (Informações podem ser buscadas no mvn repository)-->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
        </dependencies>
</project>
```

## Automatizando um comandos e plugins

Iremos configurar para que sempre que o comando mvn verify seja executado, por trás dos panos ele utilize a ferramenta PMD para verificar erros no projeto e gerar um relatório.

O goal check trava o build caso um problema esperado aconteça. O goal pmd gera o relatório no diretório target/site.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
        <!-- Versão do arquivo XML-->
	<modelVersion>4.0.0</modelVersion>
        <!-- Caminho inteiro do projeto-->
	<groupId>br.com.rafael.maven</groupId>
        <!-- Nome artifactId-->
	<artifactId>produtos</artifactId>
        <!-- Formato que o projeto será empacotado -->
	<packaging>jar</packaging>
        <!-- Versão do projeto -->
	<version>1.0-SNAPSHOT</version>
        <!-- Nome "bonitinho" para o projeto -->
	<name>produtos</name>
        <!-- Site do seu projeto -->
	<url>http://maven.apache.org</url>
	<dependencies>
                <!-- Dependência (Informações podem ser buscadas no mvn repository)-->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
        </dependencies>

        <!-- Especifica a fase de build -->
        <build>            
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-pmd-plugin</artifactId>
                    <version>3.13.0</version>
                    <!-- Especificações de coisas a serem executadas -->
                    <executions>
                        <execution>
                            <!-- Quando será executado -->
                            <phase>verify</phase>
                            <!-- Comandos do plugin -->
                            <goals>
                                <goal>check</goal>
                                <goal>pmd</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
                <plugin>
                        <groupId>org.jacoco</groupId>
                        <artifactId>jacoco-maven-plugin</artifactId>
                        <version>0.8.6-SNAPSHOT</version>
                        <executions>
                                <execution>
                                        <goals>
                                                <goal>prepare-agent</goal>
                                                <goal>report</goal>
                                        </goals>
                                </execution>
                        </executions>
                </plugin>
            </plugins>
        </build>
</project>
```

## Utilizando plugin JaCoCo para verificar a cobertura de testes

Executar o comando com cmd aberto no diretório do projeto.

```
mvn jacoco:help
```

Configurar para rodar o JaCoCo ao executar mvn verify, arquivo também é gerado no diretório targer/site:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
        <!-- Versão do arquivo XML-->
	<modelVersion>4.0.0</modelVersion>
        <!-- Caminho inteiro do projeto-->
	<groupId>br.com.rafael.maven</groupId>
        <!-- Nome artifactId-->
	<artifactId>produtos</artifactId>
        <!-- Formato que o projeto será empacotado -->
	<packaging>jar</packaging>
        <!-- Versão do projeto -->
	<version>1.0-SNAPSHOT</version>
        <!-- Nome "bonitinho" para o projeto -->
	<name>produtos</name>
        <!-- Site do seu projeto -->
	<url>http://maven.apache.org</url>
	<dependencies>
                <!-- Dependência (Informações podem ser buscadas no mvn repository)-->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
        </dependencies>

        <!-- Especifica a fase de build -->
        <build>            
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-pmd-plugin</artifactId>
                    <version>3.13.0</version>
                    <!-- Especificações de coisas a serem executadas -->
                    <executions>
                        <execution>
                            <!-- Quando será executado -->
                            <phase>verify</phase>
                            <!-- Comandos do plugin -->
                            <goals>
                                <goal>check</goal>
                                <goal>pmd</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
                <plugin>
                        <groupId>org.jacoco</groupId>
                        <artifactId>jacoco-maven-plugin</artifactId>
                        <version>0.8.6-SNAPSHOT</version>
                        <executions>
                                <execution>
                                        <goals>
                                                <goal>prepare-agent</goal>
                                                <goal>report</goal>
                                        </goals>
                                </execution>
                        </executions>
                </plugin>
            </plugins>
        </build>
</project>
```

## Criando projeto Web

Para criar projeto Web.

1. Criar projeto Maven utilizando archetype de projeto Web maven-archetype-webapp.
2. Adicionar plugin Java Servlet API:
```xml
<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>javax.servlet-api</artifactId>
	<version>3.1.0</version>
	<scope>provided</scope>
</dependency>
```
3. Atualizar a versão no web.xml (Pesquisar na internet)
4. Alterar versão do maven compiler no seu pom.xml pra sua versão java:
```xml
<properties>
	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	<maven.compiler.source>1.8</maven.compiler.source>
	<maven.compiler.target>1.8</maven.compiler.target>
</properties>
```
5. Projeto > Propriedades > Project Facets > "Conferir versão do Java".
6. Adicionar plugin maven para adicionar um servidor para rodar a aplicação, no caso de usar o Jetty:
6.1. Executar o comando: **mvn jetty:run**

Observação: para parar o Jetty você pode executar **CRTL+C**.

## Adição de nova página via classe HttpServlet:

```java
package src.main.java;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/contato")
public class ContatoServlet extends HttpServlet {
	private static final long serialVersionUID = 1755493798575605972L;

	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		PrintWriter writer = resp.getWriter();
		writer.println("<html><h2>Contato!</h2></html>");
		writer.close();
	}
}
```

## Geração do compilado do projeto web .war

Rodar o seguinte comando com o cmd aberto no diretório do projeto: 

```
mvn package
```

É boa prática dar um clean antes do package para garantir a não existência de algo indesejado:

```
mvn clean package
```

## Tipos de Escopo de Dependência

Há cinco tipos de escopo: **compile, runtime, test, provided e system**.


**compile**: Se nenhum escopo for especificado para uma dependência, compile é o padrão. Se uma dependência tem o escopo compile, ela será incluída em todos os classpaths do projeto. Transitivo

**runtime**: Uma dependência com o escopo runtime é necessária na execução e nos testes, mas não na compilação das classes. Por consequência, a dependência é incluída nos classpaths dessas duas fases. Transitivo

**test**: O escopo test deve ser especificado nas dependências que são utilizadas nas classes de teste. Nos tutoriais anteriores, quando criamos projetos com o archetype Quickstart, o JUnit já era incluído com esse escopo. Uma dependência com o escopo test é incluída na compilação e execução dos testes. Não-Transitivo

**provided**: Se uma dependência tem o escopo provided, assume-se que ela será fornecida pelo ambiente de execução onde o projeto será compilado e executado. Por exemplo, a Servlet API geralmente deve ser declarada com o escopo provided, pois o Web Container contém e utiliza o arquivo JAR da API na compilação e tempo de execução. Não-Transitivo

**system**: O escopo system é similar ao provided, a diferença é que o caminho do artefato deve ser especificado na declaração da dependência(através da tag systemPath). Devido a isso, perceba que, ao menos em um ambiente totalmente controlado, esse escopo pode levar a sérios problemas de portabilidade. Não-Transitivo

A partir da versão 2.0.9 do Maven, um tipo de escopo especial foi incluído: o **import**. O escopo import é utilizado especificamente no gerenciamento de dependências em projetos com muitos módulos, com o intuito de evitar declarações da mesma dependência espalhadas nos vários arquivos POM do projeto. Como a explicação desse escopo requer alguns exemplos para ficar mais clara, deixaremos esse assunto para outro post.

## Utilizando dependências de projetos pessoais

Você pode adicionar uma dependência de um projeto existente em sua máquina da mesma forma que utiliza as da internet.

e.g:

```xml
<dependency>
        <groupId>br.com.rafael.projeto</groupId>
        <artifactId>loja</artifactId>
        <version>1.0.0-SNAPSHOT</version>
<dependency>
```

Se o projeto adicionado como dependência estiver na mesma workspace do Eclipce, nas dependências do Maven será referenciado o seu projeto em si e não o .jar do mesmo. Para que seja compilado e executado com sucesso, é necessário ir até o projeto que é dependente e instalar o .jar em seu diretório local com o comando:

```
mvn install
```

Se o projeto adicionado como dependência estiver na mesma workspace do Eclipce, nas dependências do Maven será referenciado o .jar do projeto.

---
## Referências:

#### Conteúdo de estudo:
Cursos da Alura.

#### Tipos de dependências: 
Anderson Gomes - [Maven] Tipos de Escopo de Dependência
https://medium.com/@andgomes/tipos-de-escopo-de-depend%C3%AAncia-4ef1168ee5dd