# maven-packages

This repository contains the Maven libraries that I created. They're hosted on GitHub Packages. [Here's the full list](https://github.com/axel-op/maven-packages/packages).

Below are the instructions to use them in your Java project.

## Authenticating to GitHub Packages

This is a **one-time setup to use any Maven artifact from GitHub Packages**.

You must [create a Personal Access Token (PAT)](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token), with at least the [`read:packages` scope](https://docs.github.com/en/packages/learn-github-packages/about-permissions-for-github-packages#about-scopes-and-permissions-for-package-registries).
It is required to install any library from GitHub Packages, [even if it's public](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages#authenticating-to-github-packages).

### On your local computer

Add your credentials to GitHub Packages in your [`settings.xml`](https://maven.apache.org/settings.html) file:  

```xml
<!-- settings.xml -->
<settings>
  
  <servers>
    <server>
      <id>github-packages</id> <!-- you'll use the same ID in your pom.xml -->
      <username>${YOUR_GITHUB_USERNAME}</username> <!-- for example: axel-op -->
      <password>${YOUR_GITHUB_PAT}</password>
    </server>
  </servers>
  
</settings>
```

### In a GitHub Actions workflow

```yml
jobs:
  your-job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Maven Central Repository
        uses: actions/setup-java@v3
        with:
          java-version: '11'
          server-id: github-packages # you'll use the same ID in your pom.xml
          server-username: MAVEN_USERNAME
          server-password: MAVEN_PASSWORD
      - run: mvn test # or whatever command you want to run
        env:
          MAVEN_USERNAME: ${{ secrets.GITHUB_USERNAME }}
          MAVEN_PASSWORD: ${{ secrets.GITHUB_PAT }}
```

[Create secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) to encrypt your username and your PAT.

## Adding a dependency in your `pom.xml`

Add a reference to this repository in your [`pom.xml`](https://maven.apache.org/pom.html#Repositories):

```xml
<!-- pom.xml -->
<project>
  
  <repositories>
    <repository>
      <id>github-packages</id> <!-- use the same id as in the previous step -->
      <name>axel-op Maven libraries</name>
      <url>https://maven.pkg.github.com/axel-op/maven-packages</url>
    </repository>
  </repositories>
    
</project>
```

You can now add a dependency to [any Maven artifact in this repository](https://github.com/axel-op/maven-packages/packages)! For example:

```xml
<!-- pom.xml -->
<project>
  
  <dependencies>
    <dependency>
      <groupId>fr.axelop.agnosticserverlessfunctions</groupId>
      <artifactId>agnostic-serverless-functions-interfaces</artifactId>
      <version>0.0.1-SNAPSHOT</version>
    </dependency>
  </dependencies>
    
</project>
```
