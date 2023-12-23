# MavenDependencyCheck
An automation script to run [OWASP Dependency-Check](https://www.owasp.org/index.php/OWASP_Dependency_Check) on multiple Maven Based projects.

This script basically clones the given repositories and builds them using maven. Once successful, it runs dependency-check on them and generates the reports

## Requirements
* Python modules: [os](https://docs.python.org/2/library/os.html) & [shutil](https://docs.python.org/2/library/shutil.html)
* Maven: Installation instructions can be found [here](https://maven.apache.org/install.html)
* [``` repo.conf```](https://github.com/security-prince/MavenDependencyCheck/blob/master/repo.conf) containing the git commands to be run for cloning the projects

Example commands for ```repo.conf```
 
 ```git clone https://github.com/elderstudios/uni-dvwa-spring.git```
 
## Usage
```python depcheck.py```

And let the script do the magic  

##### Tested and working fine on CentOS Linux release 7.6.1810 (Core), Mac and Windows with Python 3.7 or above.  
 
Note: Dependency check might need internet access to update the NVD Database for which a proxy might needed if you are in a restricted environment. To configure this script to use proxy for this use this sample code to configure your proxy settings and uncomment lines from [85-88](https://github.com/security-prince/MavenDependencyCheck/blob/master/depcheck.py#L85) and comment out line [56](https://github.com/security-prince/MavenDependencyCheck/blob/master/depcheck.py#L56). Refer: [Dependency check Command Line Arguments](https://jeremylong.github.io/DependencyCheck/dependency-check-cli/arguments.html)  
For running the mvn command using a proxy refer this [article](https://medium.com/@petehouston/execute-maven-behind-a-corporate-proxy-network-5e08d075f744)  

### NVD API Key Highly Recommended

With 9.0.0 and above dependency-check has moved from using the NVD data-feed to the NVD API.
Users of dependency-check are **highly** encouraged to obtain an NVD API Key; see https://nvd.nist.gov/developers/request-an-api-key
Without an NVD API Key dependency-check's updates will be **extremely slow**.
Please see the documentation for the cli, maven, gradle, or ant integrations on
how to set the NVD API key.

## Supported report formats
* XML
* HTML
* CSV
* JSON
* JUNIT
* SARIF    
*Note: By default the script generates reports in all the formats, individual report format can be set using the ```-f``` or ```--format``` arguments on line [91](https://github.com/security-prince/MavenDependencyCheck/blob/master/depcheck.py#L91).*

## Authors
* [Praveen Sutar](https://twitter.com/praveensutar123)  
* [Ishaq Mohammed](https://twitter.com/security_prince)
* [Devaraju Garigapati](https://www.linkedin.com/in/devaraju-garigapati-561a9128a/)  

## Credits
* [OWASP Dependency Check](https://www.owasp.org/index.php/OWASP_Dependency_Check) by [Jeremy Long](https://twitter.com/ctxt)  
* [Shrutirupa Banerjiee](https://twitter.com/freak_crypt) & [Aishwarya Iyer](https://twitter.com/infosecpanda) for reviewing  


##### Pull Requests and comments are welcome :relaxed:  
##### Also I know there is a [maven plugin](https://jeremylong.github.io/DependencyCheck/dependency-check-maven/) available for dependency check which can directly be injected to the project's pom.xml, but the use case for me was such that I did not have write access to the code repo and injecting the maven script for dependency check after cloning the projects and then building them was a bit time consuming.

