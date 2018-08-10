************
jvmtop 실행
************


jvmtop.sh 실행
==================

* 윈도우즈가 아닌 모든 상황에서는 jvmtop.sh 파일을 실행하면 된다.

단, 해당 사용자 계정에 JAVA_HOME 값이 설정되어 있어야만 정상적으로 수행한다.

.. code-block:: console

    $ ./jvmtop.sh
     JvmTop 0.8.0 alpha - 12:20:51,  amd64,  4 cpus, Linux 2.6.32-64, load avg 0.00
     http://code.google.com/p/jvmtop
    
      PID MAIN-CLASS      HPCUR HPMAX NHCUR NHMAX    CPU     GC    VM USERNAME   #T DL
    29995 m.jvmtop.JvmTop   25m 1751m   10m  130m  1.83%  0.00% S6U26   i*****   28
     2943 artup.Bootstrap   52m 1751m   74m   n/a  1.52%  0.00% O8U12   i*****   42
    30054 outer.boot.Boot    7m 1751m   12m  130m  1.28%  0.00% S6U26   i*****   14
    14894 pm-server.jar    146m  910m   88m   n/a  0.89%  0.00% O8U12   i*****   55
    10929 artup.Bootstrap   49m 1820m   88m   n/a  0.47%  0.00% O8U12   i*****   56
    31254 agg.jar          444m 1751m   47m  130m  0.46%  0.00% O7U80   i*****   40
    16815 artup.Bootstrap   13m 1751m   35m  304m  0.44%  0.00% S6U26   i*****   31
    13067 artup.Bootstrap  147m  910m  206m 1072m  0.23%  0.00% S6U26   i*****   64
    20079 spring-boot.jar   29m  910m   83m   n/a  0.22%  0.00% O8U16   i*****   28

* 아무 옵션 없이 jvmtop을 실행하면 전체 자바 프로세스의 목록만 나타난다

프로세스의 쓰레드 모니터링
======================================

* 프로세스의 CPU를 점유하는 쓰레드를 모니터링하고 싶으면, jvmtop 의 명령어 가장 뒤에 pid(프로세스id)를 명시해 주면 된다

.. code-block:: console

    $ ./jvmtop.sh 2943
     JvmTop 0.8.0 alpha - 12:33:40,  amd64,  4 cpus, Linux 2.6.32-64, load avg 0.00
     http://code.google.com/p/jvmtop

     PID 2943: org.apache.catalina.startup.Bootstrap
     ARGS: start
     VMARGS: -Djava.util.logging.config.file=/home1/irteam/apps/tom[...]
     VM: Oracle Corporation Java HotSpot(TM) 64-Bit Server VM 1.8.0_121
     UP: 404:43m #THR: 42   #THRPEAK: 42   #THRCREATED: 48   USER: irteam
     GC-Time:  0: 0m   #GC-Runs: 19        #TotalLoadedClasses: 9600
     CPU:  1.18% GC:  0.00% HEAP:  74m /1751m NONHEAP:  76m /  n/a

      TID   NAME                                    STATE    CPU  TOTALCPU BLOCKEDBY
         55 RMI TCP Connection(2)-10.161.6       RUNNABLE  1.65%     0.05%
         56 JMX server connection timeout   TIMED_WAITING  0.11%     0.00%
         48 http-nio-10424-AsyncTimeout     TIMED_WAITING  0.00%     3.49%
         11 AsyncFileHandlerWriter-1229416  TIMED_WAITING  0.00%     4.86%
         31 http-nio-10425-ClientPoller-0        RUNNABLE  0.00%     3.82%
         32 http-nio-10425-ClientPoller-1        RUNNABLE  0.00%     3.79%
         45 http-nio-10424-ClientPoller-0        RUNNABLE  0.00%     3.80%
         34 http-nio-10425-AsyncTimeout     TIMED_WAITING  0.00%     3.50%
         13 NioBlockingSelector.BlockPolle       RUNNABLE  0.00%     3.35%
         14 NioBlockingSelector.BlockPolle       RUNNABLE  0.00%     3.42%

* 어떤 쓰레드가 CPU 를 가장 많이 사용하고 있는지 확인이 가능하다.


프로세스의 메소드 모니터링
======================================


* 프로세스의 CPU 를 점유하는 메소드를 모니터링하고 싶으면 --profile 옵션과 함께 pid(프로세스id)를 명시해 주면 된다

.. code-block:: console

    $ ./jvmtop.sh --profile 2943
     JvmTop 0.8.0 alpha - 14:13:51,  amd64,  4 cpus, Linux 2.6.32-64, load avg 0.20
     http://code.google.com/p/jvmtop

     Profiling PID 2943: org.apache.catalina.startup.Bootstrap st

      52.98% (     0.37s) ....google.api.client.http.apache.ApacheHttpRequest.exec()
      26.15% (     0.18s) ...qos.logback.core.recovery.ResilientOutputStreamBase.f()
      11.84% (     0.08s) ch.qos.logback.classic.spi.CallerData.extract()
       7.01% (     0.05s) ....google.api.client.http.apache.ApacheHttpTransport.ne()
       2.02% (     0.01s) org.springframework.util.StreamUtils.copy()

* 어떤 메소드가 가장 CPU 를 많이 점유했는지 확인이 가능하다.
