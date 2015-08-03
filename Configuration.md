## Configuration parameters ##

> The parameters to configure obligatorily are the follow:
  * **_List of grinder properties_** that control The Grinder worker and agent processes.

  * **_jython test file_** is the test that you want to run.

> May be configured also optionals parameters into your Maven project POM file:
    * **daemon\_option** -- the default value is FALSE. If it is set TRUE the agent goal run agent process with **_-daemon_** option;
    * **daemon\_period** -- the default value is 60 seconds. If daemon\_option is TRUE indicates the agent sleep time;

## How to configure plugin ##

> In order to use this plugin add the following dependency to **`<plugins>`** section of POM file into your Maven project:
```
    <build>
        <plugins>
            ...
	    <plugin>
		<groupId>com.fides</groupId>
		<artifactId>grinderplugin</artifactId>
		<version>0.0.1-SNAPSHOT</version>
            </plugin>
            ...
        </plugins>
    </build>
```
> The **_grinder properties file_** and **_jython test file_** may be configured from both configuration directory and POM file of your Maven project.

> POM properties **always overwrites** the same properties of grinder properties file.

> ### Configuration directory ###

  * Create the **grinder properties file** and name it as you want. The extension of file must be **.properties**;

  * Create the following directories into your Maven project directory:
    * src/test/config
    * src/test/jython

  * Copy **grinder properties file** and **jython test file** into the new directories as follow:
```
     ---------------------------
    |  Maven project directory  |
     ---------------------------
                  |
                  |    -----
                  |---| src |
                       -----
                         |
                         |    ------
                         |---| test |
                              ------
                                 |
                                 |    --------
                                 |---| config |
                                 |    --------
                                 |       |
                                 |       |--- grinder properties file
                                 |
                                 |    --------
                                 |---| jython |
                                      --------
                                         |
                                         |--- jython test file
                                 
```
  * **config and jython directories can not contain others files.**

  * Check that jython test is named as the value of grinder property **grinder.script**. If it is not configured, name the file with the default name **grinder.py**;

  * Set optionals parameters, if you need;

  * Install the plugin into your Maven repository executing the follow command-line in the directory of your Maven project:
```
    mvn install
```

> ### POM file ###

  * Set **`<configuration>`** section of the grinderplugin dependency as followed:
```
    <plugin>
		<groupId>com.fides</groupId>
		<artifactId>grinderplugin</artifactId>
		<version>0.0.1-SNAPSHOT</version>
                <configuration>
				<path>................</path>
				<pathTest>............</pathTest> 
				<daemon_option>.......</daemon_option>
				<daemon_period>.......</daemon_period>
				<properties>
				 .....
				</properties>
		</configuration>
    </plugin>
```
  * **path**          -- absolute path of **_grinder properties file_**;
  * **pathTest**      -- absolute path of jython test **_directory_**;
  * **daemon\_option** -- enable/disable agent daemon option (OPTIONAL);
  * **daemon\_period** -- agent sleep time (OPTIONAL);
  * **properties**    -- list of grinder properties. You can set property as `<name_property>`value`<\name_property>`.
> For example, to set grinder property grinder.runs = 10, add line to **`<properties>`** section as follow:
```
     <properties>
        ...
	<grinder.runs>10</grinder.runs>
        ...
     </properties>
```

  * Install the plugin into your Maven repository executing the follow command-line in the directory of your Maven project:
```
    mvn install
```


## Configuration examples ##

> ### Configure plugin from POM file ###

> #### Example 1 ####
    * Configuration parameters:
      * **`<path>`** : grinder properties file ;
      * **`<pathTest>`** : jython test file;
      * **Agent daemon option** : default value (FALSE). Run default agent;
      * **Agent sleep time** : is not significant because agent daemon option is FALSE;
      * **`<properties>`** : not defined;
```
    <plugin>
		<groupId>com.fides</groupId>
		<artifactId>grinderplugin</artifactId>
		<version>0.0.1-SNAPSHOT</version>
                <configuration>
				<path>C:\Documents and Settings\grinder.properties</path>
				<pathTest>C:\Documents and Settings\JythonTests</pathTest> 
		</configuration>
    </plugin>
```

> #### Example 2 ####
    * Configuration parameters:
      * **`<path>`** : grinder properties file ;
      * **`<pathTest>`** : jython test file;
      * **Agent daemon option** : run agent with -daemon option;
      * **Agent sleep time** : overwrite default sleep time (60000 ms);
      * **`<properties>`** : grinder.runs and grinder.script properties of the grinder properties file are overwrite;
```
    <plugin>
		<groupId>com.fides</groupId>
		<artifactId>grinderplugin</artifactId>
		<version>0.0.1-SNAPSHOT</version>
                <configuration>
				<path>C:\Documents and Settings\grinder.properties</path>
				<pathTest>C:\Documents and Settings\JythonTests</pathTest> 
				<daemon_option>true</daemon_option>
				<daemon_period>5000</daemon_period>
				<properties>
				     <grinder.runs>5</grinder.runs>
                                     <grinder.script>test.py</grinder.script>
				</properties>
		</configuration>
    </plugin>
```