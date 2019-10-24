# Ejemplo uso plugin de maven JGit-Flow para trabajo con ramas Git siguiendo el flujo [git-flow](http://aprendegit.com/que-es-git-flow/)

El proyecto es [Maven](http://maven.apache.org) y muestra el uso del plugin [JGit-Flow](https://bitbucket.org/atlassian/jgit-flow/wiki/Home) de [Atlassian](https://www.atlassian.com).

## Configuración del POM.xml

El plugin es sencillo de configurar en nuestro proyecto. Por un lado es necesario incluir la información SCM:

```xml
<scm>
  <connection>scm:git:https://github.com/juanmacintas/demo-jgitflow-maven-plugin.git</connection>
  <developerConnection>scm:git:https://github.com/juanmacintas/demo-jgitflow-maven-plugin.git</developerConnection>
  <url>https://github.com/juanmacintas/demo-jgitflow-maven-plugin</url>
  <tag>HEAD</tag>
</scm>
```
y añadir la información del plugin y su configuración:

```xml
<plugin>
  <groupId>external.atlassian.jgitflow</groupId>
  <artifactId>jgitflow-maven-plugin</artifactId>
  <version>1.0-m5.1</version>
  		<configuration>
        	<username>${git.user}</username>
        	<password>${git.password}</password>
        	<autoVersionSubmodules>true</autoVersionSubmodules>
        	<pushFeatures>true</pushFeatures>
        	<pushReleases>true</pushReleases>
        	<pushHotfixes>true</pushHotfixes>
        	<noDeploy>true</noDeploy>
        	<releaseBranchVersionSuffix>RC</releaseBranchVersionSuffix>
        	<flowInitContext>
						<masterBranchName>master</masterBranchName>
						<developBranchName>develop</developBranchName>
						<featureBranchPrefix>feature/</featureBranchPrefix>
						<releaseBranchPrefix>release/</releaseBranchPrefix>
						<hotfixBranchPrefix>hotfix/</hotfixBranchPrefix>
        	</flowInitContext>
		</configuration>
</plugin>
```

Para obtener información sobre todos los parámetros de configuración es posible acceder a la [WIKI](https://bitbucket.org/atlassian/jgit-flow/wiki/Home) de jgit-flow. 

| Option              | Description                                                                                                                                     |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| noDeploy            | Lo seteamos a `true` para que el plugin plugin no ejecute `mvn deploy`. Solo realizará `mvn install`. |
| username            | Usuario del repositorio que va a hacer uso del plugin. |
| password    		  | Password del usuario del repositorio que va a hacer uso del plugin
|releaseBranchVersionSuffix| Sufijo para las release branches |
|masterBranchName | Nombre de la rama maestra |
|developBranchName| Nombre de la rama de desarrollo |
|featureBranchPrefix | Prefijo para las ramas de features |
|releaseBranchPrefix | Prefijo para las ramas de release |
|hotfixBranchPrefix | Prefijo para las ramas de hotfix |

## Creación de una nueva Release

### Desde la rama de Desarrollo(develop)


Estos son los pasos a realizar para crear una nueva rama de release:
 
1.  Clonar el repositorio
2.  Hacer Checkout sobre la rama de desarrollo
3.  Ahora, ya es posible crear la release mediante el comando siguiente:
```bash
mvn Dgit.user=usuario -Dgit.password=passwordjgitflow:release-start
```
4.  Este comando creará la nueva rama de release con origen develop, solicitando introducir algunos parámetros como el nombre de la release. Automaticamente hará checkout sobre la nueva rama creada.
5. Realice los commits con los cambios necesarios en la nueva rama.
6.  Cuando esté todo terminado, puedo terminar la release. Para ello se ejecutará el siguiente comando:
```bash
mvn -Dgit.user=usuario -Dgit.password=password jgitflow:release-finish
```
7.  Al finalizar los comandos (si no hay que realizar ningún merge) se habrá actualizado la  rama de develop y la master con los cambios.


## Creación de una nueva Feature

### Desde la rama de Desarrollo(develop)

Estos son los pasos a realizar para crear una nueva rama de feature:
 
1.  Clonar el repositorio
2.  Hacer Checkout sobre la rama de desarrollo
3.  Ahora, ya es posible crear la feature mediante el comando siguiente:
```bash
mvn Dgit.user=usuario -Dgit.password=passwordjgitflow:feature-start
```
4.  Este comando creará la nueva rama de feature con origen develop, solicitando introducir algunos parámetros como el nombre de la feature. Automaticamente hará checkout sobre la nueva rama creada.
5. Realice los commits con los cambios necesarios en la nueva rama.
6.  Cuando esté todo terminado, puedo terminar la release. Para ello se ejecutará el siguiente comando:
```bash
mvn -Dgit.user=usuario -Dgit.password=password jgitflow:feature-finish
```
7.  Al finalizar la ejecución (si no hay que realizar ningún merge) se habrá actualizado la  rama de develop con los cambios.

## Creación de un nuevo Hot-Fix

### Desde la rama master

Estos son los pasos a realizar para crear una nueva rama de hot-fix:
 
1.  Clonar el repositorio
2.  Hacer Checkout sobre la rama master
3.  Ahora, ya es posible crear la rama de hot fix mediante el comando siguiente:
```bash
mvn Dgit.user=usuario -Dgit.password=passwordjgitflow:hotfix-start
```
4.  Este comando creará la nueva rama de hotfix con origen master, solicitando introducir algunos parámetros como el nombre de la rama. Automaticamente hará checkout sobre la nueva rama creada.
5. Realice los commits con los cambios necesarios en la nueva rama.
6.  Cuando el desarrollo esté finalizado, podemos finalizar el hot-fix ejecutando el siguiente comando:
```bash
mvn -Dgit.user=usuario -Dgit.password=password jgitflow:hotfix-finish
```
7.  Al finalizar la ejecución (si no hay que realizar ningún merge) se habrá actualizado la  rama master con los cambios.
8.  Para llever estos cambios las distintas ramas es posible ejecutar el comando push.
```bash
git push origin develop
git push --tags
```
