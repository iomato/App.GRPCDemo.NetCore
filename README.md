# App.GRPCDemo.NetCore
1.����packages\Grpc.Tools\1.0.0\tools\windows_x64\protoc.exe��������
��ʼ����cmd,ת�� App.RPCDemo\proto Ŀ¼����
--plugin=protoc-gen-grpc ֵΪgrpc_csharp_plugin.exe�ļ���·��

protoc.exe --csharp_out=d:\grpcdemo\code\ --grpc_out=d:\grpcdemo\code\ --plugin=protoc-gen-grpc=C:\Users\liuyuhua\.nuget\packages\Grpc.Tools\1.0.0\tools\windows_x64\grpc_csharp_plugin.exe result.proto
protoc.exe --csharp_out=d:\grpcdemo\code\ --grpc_out=d:\grpcdemo\code\ --plugin=protoc-gen-grpc=C:\Users\liuyuhua\.nuget\packages\Grpc.Tools\1.0.0\tools\windows_x64\grpc_csharp_plugin.exe RPCDemoService.proto

�����ɵ��ļ�copy��App.RPCDemo������ 