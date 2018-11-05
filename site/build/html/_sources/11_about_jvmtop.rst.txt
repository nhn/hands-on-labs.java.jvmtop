************
jvmtop이란 ?
************


개요
============

* jvmtop 은 커맨드 라인 명령어로 간단하게 자바 프로세스의 CPU 상태를 모니터링할 수 있는 도구이다


특징
======

* jvmtop 에서 측정할 수 있는 주요 상태는 다음과 같다.
    * 프로세스별 CPU 사용량
    * 쓰레드별 CPU 사용량
    * 메소드별 CPU 사용량

다운로드하기 (실습환경이 구축되어 있지 않은 경우)
=====================================================

* 아래의 URL 에 접속하여 release 탭을 누른 후 jvmtop-0.8.0.tar.gz 를 클릭하여 파일을 다운로드 한다.

.. code-block:: text

    https://github.com/patric-r/jvmtop

* 만약 별도의 서버에서 다운로드를하려면,

1. 파일의 다운로드 링크를 복사 한 후,
2. wget 명령어로 파일을 다운로드 하고,
3. 압축을 해제하면 된다.

.. code-block:: console

    $ tar zxvf jvmtop-0.8.0.tar.gz
    jvmtop.jar
    INSTALL
    jvmtop.bat
    jvmtop.sh
    $ chmod 755 jvmtop.sh
    $

* jvmtop 압축 해제된 디렉터리로 이동하면, 실행파일들과 jar 파일이 존재하는지 확인한다.

jvmtop 사용시 유의점
========================

* jvmtop 은 JVM 에 붙어서(attach) 사용하는 프로그램이기 때문에, jvmtop 을 수행한 서버 사용자 계정과 분석하고자하는 프로세스를 실행시킨 계정이 동일해야만 한다.
* jvmtop 으로 모니터링할 때에는 CPU 사용량이 증가하기 때문에, jvmtop을 CPU 리소스가 부족한 상황에서 사용하면 안된다.



