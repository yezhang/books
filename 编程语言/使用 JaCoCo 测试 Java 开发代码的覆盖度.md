# 使用 JaCoCo 测试 Java 开发代码的覆盖度

如果具有 Jar 包的源码，则可以使用 Maven 插件生成代码覆盖度。

pom.xml 文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>FormulaUtilTest</groupId>
    <artifactId>FormulaUtilTest</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <jacoco.skip.instrument>true</jacoco.skip.instrument>
    </properties>
    <build>
        <plugins>
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.2</version>
                <configuration>
                    <destFile>target/coverage-reports/jacoco-unit.exec</destFile>
                    <dataFile>target/coverage-reports/jacoco-unit.exec</dataFile>
                    <includes>
                        <include>yyssc/basecom/**</include>
                    </includes>
                    <!-- rules里面指定覆盖规则 -->
                    <rules>
                        <rule implementation="org.jacoco.maven.RuleConfiguration">
                            <element>BUNDLE</element>
                            <limits>　　
                                <!-- 指定方法覆盖到50% -->
                                <limit implementation="org.jacoco.report.check.Limit">
                                    <counter>METHOD</counter>
                                    <value>COVEREDRATIO</value>
                                    <!--<minimum>0.50</minimum>-->
                                    <minimum>0</minimum>
                                </limit>
                                <!-- 指定分支覆盖到50% -->
                                <limit implementation="org.jacoco.report.check.Limit">
                                    <counter>BRANCH</counter>
                                    <value>COVEREDRATIO</value>
                                    <!--<minimum>0.50</minimum>-->
                                    <minimum>0</minimum>
                                </limit>
                                <!-- 指定类覆盖到100%，不能遗失任何类 -->
                                <!--<limit implementation="org.jacoco.report.check.Limit">-->
                                    <!--<counter>CLASS</counter>-->
                                    <!--<value>MISSEDCOUNT</value>-->
                                    <!--<maximum>0</maximum>-->
                                <!--</limit>-->
                            </limits>
                        </rule>
                    </rules>
                </configuration>
                <executions>
                    <execution>
                        <id>jacoco-instrument</id>
                        <phase>test</phase>
                        <goals>
                            <goal>instrument</goal>
                        </goals>
                        <configuration>
                            <skip>${jacoco.skip.instrument}</skip>
                        </configuration>
                    </execution>
                    <execution>
                        <id>jacoco-initialize</id>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <!--这个check:对代码进行检测，控制项目构建成功还是失败-->
                    <!--<execution>-->
                        <!--<id>check</id>-->
                        <!--<goals>-->
                            <!--<goal>check</goal>-->
                        <!--</goals>-->
                    <!--</execution>-->
                    <!--这个report:对代码进行检测，然后生成index.html在 target/site/index.html中可以查看检测的详细结果-->
                    <execution>
                        <id>jacoco-site</id>
                        <phase>package</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>

            </plugin>

        </plugins>
    </build>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/junit/junit -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.5</version>
        </dependency>
    </dependencies>
</project>
```


如果没有 Jar 包的源码，但是可以通过 Maven  安装该 Jar 包，