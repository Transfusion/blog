title: On calling su in an Android App
url: 306.html
id: 306
categories:
  - - Programming
  - - Unix
date: 2014-05-01 18:50:56
tags:
---
[http://su.chainfire.eu/#how](http://su.chainfire.eu/#how) I noticed that [https://github.com/koush/Superuser](https://github.com/koush/Superuser)'s su binary requires quotes around the target command, or else it won't execute properly.

```bash
u0_a156@aries:/ $ su -c ping 8.8.8.8
su -c ping 8.8.8.8
Unknown id: 8.8.8.8

u0_a156@aries:/ $ su -c "ping 8.8.8.8"
su -c "ping 8.8.8.8"
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=3 ttl=39 time=262 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=39 time=271 ms
```

The "solution" is to write the intended su -c command to a shell script file and then call it with ProcessBuilder:

```java
try {
      String samplePingCommand = new String("su -c ""+"ping 8.8.8.8"+""");
      FileOutputStream fOut = getActivity().openFileOutput("test_ping.sh", MODE_WORLD_READABLE);
      OutputStreamWriter osw = new OutputStreamWriter(fOut);
      osw.write(samplePingCommand);
      osw.flush();
      osw.close();

      ProcessBuilder testPingCommand = new ProcessBuilder("sh", getActivity().getFilesDir()+"/test_ping.sh");
      testPingCommand.redirectErrorStream(true);
      Process startTestPingCommand = testPingCommand.start();

      BufferedReader testPingCommandOut = new BufferedReader(new InputStreamReader(startTestPingCommand.getInputStream()));
      String testPingCommandSingleLine;

          while ((testPingCommandSingleLine = testPingCommandOut.readLine()) != null) {
              /*Log.e("Ping Command Output", testPingCommandSingleLine); */
}
catch (Exception e) {
    Log.e("Ping Command", "Error", e);
}
```