# Ejemplo uso plugin de maven JGit-Flow para trabajo con ramas Git siguiento el flujo [git-flow](http://aprendegit.com/que-es-git-flow/)

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
