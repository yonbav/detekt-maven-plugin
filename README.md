[![Build Status](https://github.com/Ozsie/detekt-maven-plugin/actions/workflows/maven.yml/badge.svg)](https://github.com/Ozsie/detekt-maven-plugin/actions/workflows/maven.yml)
[![Deploy](https://github.com/Ozsie/detekt-maven-plugin/actions/workflows/deploy.yml/badge.svg)](https://github.com/Ozsie/detekt-maven-plugin/actions/workflows/deploy.yml)
[![codecov](https://codecov.io/gh/Ozsie/detekt-maven-plugin/branch/master/graph/badge.svg)](https://codecov.io/gh/Ozsie/detekt-maven-plugin)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FOzsie%2Fdetekt-maven-plugin.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FOzsie%2Fdetekt-maven-plugin?ref=badge_shield)
[![Maven Central](https://img.shields.io/maven-central/v/com.github.ozsie/detekt-maven-plugin.svg?label=Maven%20Central)](https://search.maven.org/search?q=g:%22com.github.ozsie%22%20AND%20a:%22detekt-maven-plugin%22)

# Detekt Maven Plugin

A maven plugin that wraps the Detekt CLI. It supports the same parameters as the Detekt CLI.

## How to use
### Basic configuration
```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.ozsie</groupId>
            <artifactId>detekt-maven-plugin</artifactId>
            <version>1.19.0</version>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals><goal>check</goal></goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```
Using the above configuration, Detekt will scan source files in _${basedir}/src_ and output the results in _${basedir}/detekt_.

All parameters available to Detekt version _1.19.0_ can be configured in
the plugin.


### Using plugin
```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.ozsie</groupId>
            <artifactId>detekt-maven-plugin</artifactId>
            <version>1.19.0</version>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals><goal>check</goal></goals>
                    <configuration>
                        <plugins>
                            <plugin>path/to/plugin.jar</plugin>
                        </plugins>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

Or

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.ozsie</groupId>
            <artifactId>detekt-maven-plugin</artifactId>
            <version>1.19.0</version>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals><goal>check</goal></goals>
                </execution>
            </executions>
            <dependencies>
                <dependency>
                    <groupId>group</groupId>
                    <artifactId>artifact</artifactId>
                    <version>version</version>
                </dependency>
            </dependencies>
        </plugin>
    </plugins>
</build>
```

## Specify report files
```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.ozsie</groupId>
            <artifactId>detekt-maven-plugin</artifactId>
            <version>1.19.0</version>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals><goal>check</goal></goals>
                    <configuration>
                        <report>
                            <report>txt:reports/detekt.txt</report>
                            <report>xml:reports/detekt.xml</report>
                        </report>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```
Alternatively, the configuration can be placed outside of the
`<executions>`. This allows the configuration be used when running goals
standalone

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.ozsie</groupId>
            <artifactId>detekt-maven-plugin</artifactId>
            <version>1.19.0</version>
            <configuration>
                <report>
                    <report>txt:reports/detekt.txt</report>
                    <report>xml:reports/detekt.xml</report>
                </report>
            </configuration>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals><goal>check</goal></goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```
## Set baseline
First a baseline file needs to be generated
```bash
mvn detekt:cb
```
This will generate a baseline file for each module named as `baseline-<module-name>.xml`. For more information on generating baselines, see [create-baseline](#create-baseline). You can now reference the baseline file in your configuration, as below.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.ozsie</groupId>
            <artifactId>detekt-maven-plugin</artifactId>
            <version>1.19.0</version>
            <configuration>
                <baseline>baseline.xml</baseline>
            </configuration>
            <executions>
                <execution>
                    <phase>verify</phase>
                    <goals><goal>check</goal></goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

### Goals
#### check

Used to run detekt. All cli parameters, excluding -gc and -cb, are available using -Ddetekt.{parameter}

_Examples_

 * `mvn detekt:check -Ddetekt.config=detekt.yml`
 * `mvn detekt:check -Ddetekt.debug=true`

#### create-baseline

Used to create a baseline. All cli parameters, excluding -gc and -cb,
are available using -Ddetekt.{parameter}. By default, a file called
baseline-<module-name>.xml will be generated. If you include -Ddetekt.baseline in the
call you can specify some other name for the baseline file.

_Examples_

*  `mvn detekt:cb -Ddetekt.config=detekt.yml`
 * `mvn detekt:cb -Ddetekt.debug=true`
*  `mvn detekt:cb -Ddetekt.baseline=some-other-baseline.xml`
*  `mvn detekt:create-baseline -Ddetekt.config=detekt.yml`
 * `mvn detekt:create-baseline -Ddetekt.debug=true`

#### generate-config

Used to generate a default configuration file

_Example_

 * `mvn detekt:gc`
 * `mvn detekt:generate-config`
 
 For more information on Detekt, have a look at https://github.com/detekt/detekt
 
## Contributors
 * [andreysaksonov](https://github.com/andreysaksonov)
 * [Geminist](https://github.com/Geminist)
 * [josephlbarnett](https://github.com/josephlbarnett)
 * [reubenfirmin](https://github.com/reubenfirmin)
 * [schalkms](https://github.com/schalkms)
 * [ThatJoeMoore](https://github.com/ThatJoeMoore)
 * [va1m](https://github.com/va1m)
 * [vladimirfx](https://github.com/vladimirfx)
 * [pinkasey](https://github.com/pinkasey)
 * [krichter722](https://github.com/krichter722)
 * [currensy](https://github.com/currensy)
 * [rgrebski](https://github.com/rgrebski)

## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FOzsie%2Fdetekt-maven-plugin.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FOzsie%2Fdetekt-maven-plugin?ref=badge_large)
