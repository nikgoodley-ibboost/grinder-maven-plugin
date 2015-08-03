# Introduction #

> The plugin consists of goals:
    * agent
    * report
    * console
    * TCPProxy


> The first step of each goal is create plugin configuration directory **target/test/config** (if do not exists) in your Maven project directory.

```
     ---------------------------
    |  Maven project directory  |
     ---------------------------
                  |
                  |    --------
                  |---| target |
                       --------
                           |
                           |    ------
                           |---| test |
                                ------
                                   |
                                   |    --------
                                   |---| config |
                                        --------
                                            |
                                            |--- grinder_agent.properties
                                            |
                                            |--- jython test
```

> Directory contents:
    * **grinder\_agent.properties** -- grinder properties configuration;
    * **jython test** -- copy of the jython test recorded by TCPProxy;

## How to run goal ##

> In order to run goal from shell:
    1. open a command-line shell;
    1. cd into your Maven project directory;
    1. execute the command-line with the sintax following:
```
    mvn groupId:artifactId:version:goal_name;
```

## Agent goal ##

> _Agent.java_ class implement agent goal.

> Execute the follow command-line to run agent goal:
```
    mvn com.fides:grinderplugin:0.0.1-SNAPSHOT:agent
```

> This goal run the grinder agent process configured. All log files generated are saved into **target/test/log\_files** directory (created if do not exists).

> The classpath is set with jython 2.2.1 version because it is used by agent process of The Grinder 3.7.1.

> Goal execution generate the follow output:
```
       ---------------------------
    |  Maven project directory  |
     ---------------------------
                  |
                  |    --------
                  |---| target |
                       --------
                           |
                           |    ------
                           |---| test |
                                ------
                                   |
                                   |    --------
                                   |---| config |
                                   |    --------
                                   |        |
                                   |        |--- grinder_agent.properties
                                   |        |
                                   |        |--- copy of jython test configured
                                   |
                                   |    -----------
                                   |---| log_files |
                                        -----------
                                            |
                                            |--- data_ file 0
                                            |    ...
                                            |    ...
                                            |--- data_ file n
                                            |
                                            |--- out_ file 0
                                            |    ...
                                            |    ...
                                            |--- out_ file n
```

> This goal may be run independently of the other.

## Report goal ##

> _Report.java_ class implement report goal.

> Control if exists log files into the log directory **target/test/log\_files**. If not exists, run agent goal to generate log files.

> Execute the follow command-line to run report goal:
```
    mvn com.fides:grinderplugin:0.0.1-SNAPSHOT:report
```

> Log directory must contain **only** log files.

> This goal run The Grinder Analyzer that create a new folder for each html report of log files into the log directory.

> The classpath is set with jython 2.5.2 version because it is used by The Grinder Analyzer.

> To create HTML reports of data files with a **minimun number of data lines**:
  * open file grinderplugin/src/main/resources/jython/conf/analyzer.properties
  * set variable **buckets** with the minimun number of data lines for data files
  * open file grinderplugin/src/main/resources/jython/analyzer.py
  * uncomment (deleting # simbol) the follow code of the method **def main():**
```
    #   if tail (log_file, CONFIG.buckets+1, ignoreBlankLines=True).__len__() < CONFIG.buckets :  
    #   logger.fatal("")
    #   logger.fatal( "FATAL: insufficient test data to graph. ")
    #   logger.fatal( "grinderplugin/src/main/resources/jython.conf/analyzer.properties specifies")
    #   logger.fatal( "       " + str(CONFIG.buckets) + " buckets, but " + filename + " contains")
    #   logger.fatal( "       less than " + str(CONFIG.buckets) + " data points.")
    #   sys.exit(1)
```
  * update the local repository executing _install_ command on grinderplugin

> Goal execution generate the follow output:
```
       ---------------------------
    |  Maven project directory  |
     ---------------------------
                  |
                  |    --------
                  |---| target |
                       --------
                           |
                           |    ------
                           |---| test |
                                ------
                                   |
                                   |    -----------------
                                   |---| grinderReport_0 |
                                   |    -----------------
                                   |    ...
                                   |    ...
                                   |    -----------------    
                                   |---| grinderReport_n |
                                        -----------------
```

> This goal may be run independently of the other goals if log directory includes log files.

## Console goal ##

> _GrinderConsole.java_ class implement console goal.

> Execute the follow command-line to run console goal:
```
    mvn com.fides:grinderplugin:0.0.1-SNAPSHOT:console
```

> This goal start graphic interface of The Grinder console.

> This goal may be run independently of the other.

## TCPProxy goal ##

> _GrinderTCPProxy.java_ class implement TCPProxy goal.

> Set your browser connection settings to specify the TCPProxy as the HTTP proxy. In the browser options dialog, set the proxy host to be the host on which the TCPProxy is running and proxy port.

> The relevant options dialog may be accessed by the following steps:
|    **Browser**      |        **Steps**                                |
|:--------------------|:------------------------------------------------|
|      MSIE           | Tools → Internet Options → Connections → Local Area Network Settings |
| Mozilla/Netscape    | Edit → Preferences → Advanced → Proxies         |
| Mozilla/Firefox     | Tools → Preferences  → Advanced → Network → Configuration |
|     Opera           | Tools → Preferences → Advanced → Network → Proxy Servers |
| Internet Explorer   | Tools → Internet Options → Connections → LAN Settings → Proxy |
| Google chrome       | Options → Change proxy settings → LAN settings → Proxy server |

> Execute the follow command-line to run TCPProxy goal:
```
    mvn com.fides:grinderplugin:0.0.1-SNAPSHOT:TCPProxy
```

> This goal create **target/test/tcpproxy** directory and run TCPProxy, with -console and -http options, to generate an HTTP script suitable for use with The Grinder.

> The jython script generated is named **grinder.py**.

> Successive execution of this goal overwrite the last test script generated.

> Goal execution generate the follow output:
```
       ---------------------------
    |  Maven project directory  |
     ---------------------------
                  |
                  |    --------
                  |---| target |
                       --------
                           |
                           |    ------
                           |---| test |
                                ------
                                   |
                                   |    ----------
                                   |---| tcpproxy |
                                        ----------
                                            |    
                                            |--- grinder.py
                                
```

> This goal may be run independently of the other.


