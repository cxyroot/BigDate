

# 启动日志分析

```shell
org.apache.catalina.startup.Bootstrap.main
org.apache.catalina.startup.Bootstrap.initClassLoaders()
org.apache.catalina.startup.Bootstrap.createClassLoader(String, ClassLoader)
org.apache.catalina.startup.ClassLoaderFactory.createClassLoader(List<Repository>, ClassLoader)
十二月 02, 2020 9:45:37 上午 org.apache.catalina.startup.ClassLoaderFactory validateFile
警告: Problem with directory [F:\Tomcat8Src\lib], exists: [false], isDirectory: [false], canRead: [false]
十二月 02, 2020 9:45:37 上午 org.apache.catalina.startup.ClassLoaderFactory validateFile
警告: Problem with directory [F:\Tomcat8Src\lib], exists: [false], isDirectory: [false], canRead: [false]
十二月 02, 2020 9:45:37 上午 org.apache.catalina.startup.ClassLoaderFactory validateFile
警告: Problem with directory [F:\Tomcat8Src\lib], exists: [false], isDirectory: [false], canRead: [false]
十二月 02, 2020 9:45:37 上午 org.apache.catalina.startup.ClassLoaderFactory validateFile
警告: Problem with directory [F:\Tomcat8Src\lib], exists: [false], isDirectory: [false], canRead: [false]
org.apache.catalina.startup.Bootstrap.createClassLoader(String, ClassLoader)
org.apache.catalina.startup.Bootstrap.createClassLoader(String, ClassLoader)
org.apache.catalina.startup.Catalina.Catalina()
org.apache.catalina.startup.Catalina.load()
org.apache.catalina.startup.Catalina.createStartDigester
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Server version:        Apache Tomcat/@VERSION@
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Server built:          @VERSION_BUILT@
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Server number:         @VERSION_NUMBER@
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: OS Name:               Windows 10
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: OS Version:            10.0
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Architecture:          amd64
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Java Home:             C:\Java\jdk1.8.0_201\jre
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: JVM Version:           1.8.0_201-b09
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: JVM Vendor:            Oracle Corporation
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: CATALINA_BASE:         F:\Tomcat8Src
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: CATALINA_HOME:         F:\Tomcat8Src
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -agentlib:jdwp=transport=dt_socket,suspend=y,address=localhost:51750
十二月 02, 2020 9:45:58 上午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -Dfile.encoding=UTF-8
十二月 02, 2020 9:45:58 上午 org.apache.catalina.core.AprLifecycleListener lifecycleEvent
信息: The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: [C:\Java\jdk1.8.0_201\bin;C:\Windows\Sun\Java\bin;C:\Windows\system32;C:\Windows;C:\Java\jdk1.8.0_201\jre\bin;C:/Java/jdk1.8.0_201/bin/../jre/bin/server;C:/Java/jdk1.8.0_201/bin/../jre/bin;C:/Java/jdk1.8.0_201/bin/../jre/lib/amd64;C:\Program Files\ibm\gsk8\lib64;C:\Program Files\ibm\gsk8\bin;C:\Program Files\VanDyke Software\Clients\;F:\JavaTools\apache-maven-3.3.9\bin;C:\Java\jdk1.8.0_201\bin;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\iCLS\;C:\Program Files\Intel\Intel(R) Management Engine Components\iCLS\;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\nodejs\;C:\TortoiseSVN\bin;C:\Program Files\Git\cmd;C:\Users\EDZ\AppData\Local\Microsoft\WindowsApps;;C:\Users\EDZ\AppData\Local\Programs\Microsoft VS Code\bin;C:\Users\EDZ\AppData\Roaming\npm;E:\eclipsePicc;;.]
十二月 02, 2020 9:45:59 上午 org.apache.coyote.AbstractProtocol init
信息: Initializing ProtocolHandler ["http-nio-8080"]
十二月 02, 2020 9:45:59 上午 org.apache.tomcat.util.net.NioSelectorPool getSharedSelector
信息: Using a shared selector for servlet write/read
十二月 02, 2020 9:45:59 上午 org.apache.coyote.AbstractProtocol init
信息: Initializing ProtocolHandler ["ajp-nio-8009"]
十二月 02, 2020 9:45:59 上午 org.apache.tomcat.util.net.NioSelectorPool getSharedSelector
信息: Using a shared selector for servlet write/read
十二月 02, 2020 9:45:59 上午 org.apache.catalina.startup.Catalina load
信息: Initialization processed in 1434 ms
```

# 加载web工程分析

```shell
#部署项目
deployApps....
#开始部署
十二月 02, 2020 9:20:48 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deploying web application directory [F:\Tomcat8Src\webapps\docs]
org.apache.catalina.core.StandardContext.startInternal
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/docs].StandardWrapper[default]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/docs].StandardWrapper[jsp]]
十二月 02, 2020 9:20:50 上午 org.apache.jasper.servlet.TldScanner scanJars
信息: At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deployment of web application directory [F:\Tomcat8Src\webapps\docs] has finished in [1,264] ms
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deploying web application directory [F:\Tomcat8Src\webapps\host-manager]
org.apache.catalina.core.StandardContext.startInternal
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/host-manager].StandardWrapper[default]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/host-manager].StandardWrapper[jsp]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/host-manager].StandardWrapper[HostManager]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/host-manager].StandardWrapper[HTMLHostManager]]
十二月 02, 2020 9:20:50 上午 org.apache.jasper.servlet.TldScanner scanJars
信息: At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deployment of web application directory [F:\Tomcat8Src\webapps\host-manager] has finished in [87] ms
#开始部署
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deploying web application directory [F:\Tomcat8Src\webapps\manager]
org.apache.catalina.core.StandardContext.startInternal
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/manager].StandardWrapper[Status]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/manager].StandardWrapper[default]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/manager].StandardWrapper[jsp]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/manager].StandardWrapper[JMXProxy]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/manager].StandardWrapper[HTMLManager]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/manager].StandardWrapper[Manager]]
十二月 02, 2020 9:20:50 上午 org.apache.jasper.servlet.TldScanner scanJars
信息: At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deployment of web application directory [F:\Tomcat8Src\webapps\manager] has finished in [20] ms

#开始部署
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deploying web application directory [F:\Tomcat8Src\webapps\ROOT]
org.apache.catalina.core.StandardContext.startInternal
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[].StandardWrapper[default]]
org.apache.catalina.core.ContainerBase.startInternal
Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[].StandardWrapper[jsp]]
十二月 02, 2020 9:20:50 上午 org.apache.jasper.servlet.TldScanner scanJars
信息: At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.
十二月 02, 2020 9:20:50 上午 org.apache.catalina.startup.HostConfig deployDirectory
信息: Deployment of web application directory [F:\Tomcat8Src\webapps\ROOT] has finished in [14] ms
```

# 系统日志信息

```java
package sys;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URISyntaxException;

public class Test {
    //	java.version          Java 运行时环境版本
    //	java.vendor         Java 运行时环境供应商
    //	java.vendor.url         Java 供应商的 URL
    //	java.vm.specification.version         Java 虚拟机规范版本
    //	java.vm.specification.vendor         Java 虚拟机规范供应商
    //	java.vm.specification.name         Java 虚拟机规范名称
    //	java.vm.version         Java 虚拟机实现版本
    //	java.vm.vendor         Java 虚拟机实现供应商
    //	java.vm.name         Java 虚拟机实现名称
    //	java.specification.version         Java 运行时环境规范版本
    //	java.specification.vendor         Java 运行时环境规范供应商
    //	java.specification.name         Java 运行时环境规范名称
    //	os.name         操作系统的名称
    //	os.arch         操作系统的架构
    //	os.version         操作系统的版本
    //	file.separator         文件分隔符（在 UNIX 系统中是“ / ”）
    //	path.separator         路径分隔符（在 UNIX 系统中是“ : ”）
    //	line.separator         行分隔符（在 UNIX 系统中是“ /n ”）
    //	 
    //	java.home         Java 安装目录
    //	java.class.version         Java 类格式版本号
    //	java.class.path         Java 类路径
    //	java.library.path          加载库时搜索的路径列表
    //	java.io.tmpdir         默认的临时文件路径
    //	java.compiler         要使用的 JIT 编译器的名称
    //	java.ext.dirs         一个或多个扩展目录的路径
    //	user.name         用户的账户名称
    //	user.home         用户的主目录
    //	user.dir
	public static void main(String[] args) throws MalformedURLException, URISyntaxException {
		 
        System.out.println("java.home : "+System.getProperty("java.home"));

        System.out.println("java.class.version : "+System.getProperty("java.class.version"));

        System.out.println("java.class.path : "+System.getProperty("java.class.path"));

        System.out.println("java.library.path : "+System.getProperty("java.library.path"));

        System.out.println("java.io.tmpdir : "+System.getProperty("java.io.tmpdir"));

        System.out.println("java.compiler : "+System.getProperty("java.compiler"));

        System.out.println("java.ext.dirs : "+System.getProperty("java.ext.dirs"));

        System.out.println("user.name : "+System.getProperty("user.name"));

        System.out.println("user.home : "+System.getProperty("user.home"));

        System.out.println("user.dir : "+System.getProperty("user.dir"));

        System.out.println("package: "+Test.class.getPackage().getName());

        System.out.println("package: "+Test.class.getPackage().toString());

        String packName = Test.class.getPackage().getName();

        /*URL packurl = new URL(packName);
        System.out.println(packurl.getPath());*/

        URI packuri = new URI(packName);

        System.out.println(packuri.getPath());

        //System.out.println(packuri.toURL().getPath());

        System.out.println(packName.replaceAll("//.", "/"));

        System.out.println(System.getProperty("user.dir")+"/"+  (Test.class.getPackage().getName()).replaceAll("//.", "/")+"/");
	}
}

```

