# CPFProxyStreamServer
１．live555.sln是windows下基于live555的实时流媒体代理服务器项目.vs2015测试可用

根据实际情况修改ProxyServerMain.cpp的40行左右的代码:
string sStreamUrl2 = "rtsp://admin:admin@192.168.1.212:554/cam/realmonitor?channel=1&subtype=0";
比如海康的修改为：string sStreamUrl2 = "rtsp://admin:admin@192.168.1.212;

在ProxyServerMain.cpp的4６行左右的代码:
CMyServerMediaSession* sms2 = CMyServerMediaSession::createNew(*env, rtspServer, sStreamUrl2.c_str(), "abc.264", "", "", 554, 3, -1);
此时如果代理主机ip是192.168.10.10,
那么客户端使用rtsp://192.168.10.10/abc.264　访问
如果46行左右中的abc.264为空，则客户端只要使用rtsp://192.168.10.10　即可访问

2.testClient.sln是是windows下基于live555客户端测试项目.vs2015测试可用
如果需要可以testRTSPClient.cpp中66行增加:
Authenticator *ourAuthenticator = NULL;
在73行增加：
ourAuthenticator = new Authenticator("admin", "Password01!");
如有必要将74行：
openURL(*env, "", "rtsp://192.168.1.96:8554/abc.264");
改为：
	openURL(*env, "", "rtsp://192.168.90.241");
  
将192行：
rtspClient->sendDescribeCommand(continueAfterDESCRIBE);
改为：
rtspClient->sendDescribeCommand(continueAfterDESCRIBE, ourAuthenticator);
