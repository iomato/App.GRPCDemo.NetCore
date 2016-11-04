# App.GRPCDemo.NetCore
ͨ��grpcʵ��΢������Centos 7��docker�н��в��ԣ�hosting grpc ����
����ʱ������ǽ��Ҫ������Ӧ�˿�

1.����packages\Grpc.Tools\1.0.0\tools\windows_x64\protoc.exe��������
��ʼ����cmd,ת�� App.RPCDemo\proto Ŀ¼����
--plugin=protoc-gen-grpc ֵΪgrpc_csharp_plugin.exe�ļ���·��

protoc.exe --csharp_out=d:\grpcdemo\code\ --grpc_out=d:\grpcdemo\code\ --plugin=protoc-gen-grpc=yourpath\.nuget\packages\Grpc.Tools\1.0.0\tools\windows_x64\grpc_csharp_plugin.exe result.proto
protoc.exe --csharp_out=d:\grpcdemo\code\ --grpc_out=d:\grpcdemo\code\ --plugin=protoc-gen-grpc=yourpath\.nuget\packages\Grpc.Tools\1.0.0\tools\windows_x64\grpc_csharp_plugin.exe RPCDemoService.proto

�����ɵ��ļ�copy��App.RPCDemo������ 

2.�������

  App.RPCDemoServer ����ˣ�����˵��
  host:����ip ��ַ��Ĭ��0.0.0.0
  port:���Ŷ˿ڣ�Ĭ��9007

  ������̣������������У�
  dotnet App.RPCDemoServer.dll host=192.168.4.37 port=9007
  centos 7.2 �£�Ҳ������windows ������

	[demo@node139 App.RPCDemoServer]$ dotnet App.RPCDemoServer.dll host=192.168.190.139 port=9007
	Google Grpc Starting
	RPC server 192.168.190.139 listening on port 9007
	Rpc Service started. Press Ctrl+C to shut down.

  App.RPCDemoClient �ͻ��ˣ�ѭ��2�Σ���������������Ҫ��ʱ�䣬����˵��
  host:����ip ��ַ��Ĭ��0.0.0.0
  port:���Ŷ˿ڣ�Ĭ��9007
  repeat���ظ����ô���

  [demo@node139 App.RPCDemoClient]$ dotnet  App.RPCDemoClient.dll host=192.168.190.139 port=9007 repeat=100

3.docker �²���
  ��ת��App.RPCDemoServer��Ŀ·����

	[demo@node139 App.RPCDemoServer]$ docker build -t grpcemoserver .
	Sending build context to Docker daemon 23.67 MB
	Step 1 : FROM microsoft/dotnet:1.0.1-runtime
	 ---> c0a30708437a
	Step 2 : COPY . /publish
	 ---> Using cache
	 ---> dad7441480f3
	Step 3 : WORKDIR /publish
	 ---> Using cache
	 ---> 11429a59af07
	Step 4 : EXPOSE 9007
	 ---> Using cache
	 ---> 517b063e476c
	Step 5 : CMD dotnet App.RPCDemoServer.dll
	 ---> Using cache
	 ---> db2c0debde34
	Successfully built db2c0debde34

	�������images,docker run ��docker service
	[demo@node139 App.RPCDemoServer]$ docker run --name rcpdemo -d -p 9008:9007 grpcemoserver
	b37db4b39a92256504dbe3a681d096782846bd60809f4442484c0a896067381d
	[demo@node139 App.RPCDemoServer]$ docker ps -a | grep grpc
	b37db4b39a92        grpcemoserver       "dotnet App.RPCDemoSe"   13 seconds ago      Up 7 seconds        0.0.0.0:9008->9007/tcp   rcpdemo

	�ڴ�һ����������:
	[demo@node139 App.RPCDemoClient]$ dotnet  App.RPCDemoClient.dll host=192.168.190.139 port=9008 repeat=100


