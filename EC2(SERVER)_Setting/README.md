## EC2(서버) 세팅하기

> 일단 서버를 생성을 못한다거나 접근을 할 줄 모른다면 [EC2(Server) create]()를 보고온다.

 * 여기에서는 세팅을 위해서 yum을 활용하는 방법과 일반적인 linux 환경에서 설정하는 방법 두가지를 볼 것이다.(Java와 Tomcat을 설치하는 방법)

 > 첫번째 : yum을 활용하는 방법
 >
 > 1. yum update를 위해 sudo yum update를 한다.
 > 
 > 2. 일단 Java를 먼저 깔아보겠다 명령어 창에 sudo yum list | grep java-를 입력한다. 
 > 
 > * ![1.png](/img/1.png)
 > 
 > 3. 위의 그림처럼 나올 것이다. 위에서 가장 최신 버전인 1.8.0 버전을 다운로드 받을 건데 sudo yum install java-1.8.0-openjdk.x86_64을 입력해 다운로드 받는다. 이 때, 중간에 다운로드 할 것인지 묻는데 y를 입력한다.
 > 
 > 4. 환경변수를 설정해야 한다. vi 관련 명령어들을 알면 좋겠지만 시간이 없으므로 따라하길 바란다. sudo vi /etc/profile을 입력한다.
 > 
 > 5. 그러면 자기 환경변수와 관련된 설정들이 있는 파일로 이동하면 키보드의 방향키를 이용하여 맨아래, 맨 끝으로 이동한다.
 > 
 > 6. i 버튼을 입력한다.(그냥 키보드 i를 누른다.) 그러면 insert 상태가 된다. 이 때, 맨 아래에 
 > 
 > * ![2.png](/img/2.png)
 > 
 > 6. 위의 이미지 처럼 넣는다. 후에 esc를 누르면 insert 모드가 종료되고 :wq를 입력해 vi를 종료한다.
 >
 > 7. 그리고 cat /etc/profile을 입력해 해당 내용이 수정 됐는지 확인하고 source /etc/profile을 입력해 준다.
 > 
 > 8. java는 마지막으로 java -version을 입력하면 자바 버전이 출력되는 걸 확인 할 수 있다.
 > 
 > 9. Tomcat을 설치해 보겠다. 자바와 마찬가지로 sudo yum list | grep tomcat을 입력한다.
 > 
 > * ![3.png](/img/3.png)
 > 
 > 10. 위의 그림처럼 나올텐데 이 때, sudo yum install tomcat, sudo yum install tomcat-admin-webapps, sudo yum install tomcat-webapps를 입력하여 세가지를 다운로드 한다. 톰캣도 설치가 완료 되었다. sudo systemctl start tomcat.service를 실행한다.(tomcat이 실행 되었다!!)
 > 
 > 11. 이제 해당 서버 url:8080에 들어가서 확인해 보자. 접속이 안되는 걸 확인 할 수 있다. 원인은 보안문제인데 관련해서 알아보자.
 >
 > * ![4.png](/img/4.png)
 >
 > 12. AWS 홈페이지에서 EC2에 들어가면 왼쪽에 보안그룹이 있다. 여기서 서버를 생성할 때 생성한 보안그룹(서버에 적용되어 있는 보안그룹)을 선택하면 인바운드가 있다. 클릭해서 아래에 편집을 누르자. 
 > 
 > * ![5.png](/img/5.png)
 > 
 > 13. 위와 같이 사용자 지정TCP로 규칙을 추가하고 8080 포트에 모든 ip에서 접근할 수 있게 소스를 입력한다. 그리고 저장을 하고 다시 서버 url:8080으로 접근해 보자!! 성공하는 걸 볼 수 있다!!


 > 두번째 : 일반적인 linux 환경에서 설정하는 방법
 > 
 > > 참고 : https://iamsangil.github.io/aws/16-09-13-aws2 