1.��ת��App.ThriftDemo\thrift Ŀ¼��ִ��
  thrift-0.9.3 -r --gen csharp DemoService.thrift
2.������Ŀ���������з����
  dotnet App.ThriftDemoServer.dll protocol=compact port=9090

3.���пͻ���
  dotnet App.ThriftDemoClient.dll protocol=compact port=9090 host=localhost repeat=10000