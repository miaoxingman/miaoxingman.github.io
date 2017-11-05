## Json Restful example with Jersey and Jackson

### fluent pattern
https://martinfowler.com/bliki/FluentInterface.html
http://blog.csdn.net/liangneo/article/details/5620631
https://en.wikipedia.org/wiki/Fluent_interface
### build pattern vs config object
https://stackoverflow.com/questions/3394853/builder-pattern-vs-config-object

### How to view diff in github

https://help.github.com/articles/comparing-commits-across-time/

### Maven – Always download sources and javadocs

Open your settings.xml file ~/.m2/settings.xml (create it if it doesn't exist). Add a section with the properties added. Then make sure the activeProfiles includes the new profile.

```
<settings>

   <!-- ... other settings here ... -->

    <profiles>
        <profile>
            <id>downloadSources</id>
            <properties>
                <downloadSources>true</downloadSources>
                <downloadJavadocs>true</downloadJavadocs>
            </properties>
        </profile>
    </profiles>

    <activeProfiles>
        <activeProfile>downloadSources</activeProfile>
    </activeProfiles>
</settings>
```


### API Document
* https://jersey.github.io/apidocs/1.19.1/jersey/index.html
* https://jersey.github.io/documentation/1.19.1/client-api.html


### Reference.
* https://www.nabisoft.com/tutorials/java-ee/producing-and-consuming-json-or-xml-in-java-rest-services-with-jersey-and-jackson
* http://www.mkyong.com/webservices/jax-rs/restful-java-client-with-jersey-client/
* https://jersey.github.io/documentation/latest/user-guide.html
* http://www.cnblogs.com/pixy/p/4838268.html
* http://www.codedata.com.tw/java/java-restful-1-jersey-and-jax-rs/

