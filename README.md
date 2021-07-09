This repository contains the Maven libraries that I created. They're hosted on GitHub Packages. [Here's the full list](https://github.com/axel-op/maven-packages/packages).

To use one of them in your Java project:

1. Add your credentials to GitHub Packages in your [`settings.xml`](https://maven.apache.org/settings.html) file:  

```xml
<!-- settings.xml -->
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  
  <!-- ... -->
  
  <servers>
    <!-- ... -->
    <server>
      <id>github-packages</id>
      <username>${YOUR_GITHUB_USERNAME}</username>
      <password>${YOUR_GITHUB_PAT}</password>
    </server>
  </servers>
  
</settings>
```

Your [Personal Access Token (PAT)](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) must have at least the [`read:packages` scope](https://docs.github.com/en/packages/learn-github-packages/about-permissions-for-github-packages#about-scopes-and-permissions-for-package-registries).
It is required to install any library from GitHub Packages, [even if they're public](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages#authenticating-to-github-packages).

2. Add a reference to this repository in your [`pom.xml`](https://maven.apache.org/pom.html#Repositories):  
```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  
  <!-- ... -->
  
  <repositories>
    <!-- ... -->
    <repository>
      <id>github-packages</id> <!-- Use the same id as in the first step -->
      <name>axel-op Maven libraries</name>
      <url>https://maven.pkg.github.com/axel-op/maven-packages</url>
    </repository>
  </repositories>
    
</project>
```
