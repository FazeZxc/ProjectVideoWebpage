int RcvThread();
SOCKET s;
void CChat_ServerDlg::OnBnClickedButton2()
{

WSADATA w;

int error = WSAStartup ( 0x0202,&w);
if(error)
{
    OnCancel();
}
 if (w.wVersion != 0x0202) 
{
    WSACleanup ();
    OnCancel();
}
SOCKADDR_IN addr;
addr.sin_family = AF_INET;
addr.sin_port = htons(DEFAULT_PORT);
addr.sin_addr.S_un.S_addr = htonl(INADDR_ANY);
s = socket ( AF_INET, SOCK_STREAM, IPPROTO_TCP);
     if (s == INVALID_SOCKET)
{
    OnCancel();
}
 if (bind(s, (LPSOCKADDR)&addr, sizeof(addr)) == SOCKET_ERROR)
{

    OnCancel();
}
listen (s, SOMAXCONN);
CreateThread(NULL, NULL, (LPTHREAD_START_ROUTINE) RcvThread, NULL, NULL, NULL);

int buffsize = 1024;
char msg[1024] = "a";
int marker;
}

    int RcvThread()
    {
char sbuffer[256];

char buffer[sizeof(sbuffer)] = {0};

for(;; )
{

    if(recv(s, buffer, sizeof(sbuffer), NULL) > 0)
    {
        memcpy(&sbuffer, buffer, sizeof(sbuffer));
        MessageBox(hnd,sbuffer,"message",NULL);
    }
}

return 0;
    }
Client's Source code :

SOCKET s;
void CChat_ClientDlg::OnBnClickedOk()
{

WSADATA wsadata;

int error = WSAStartup(0x0202,&wsadata);

 if (error)
{
    MessageBox("Error","ERRR");

    OnCancel();
}


if (wsadata.wVersion != 0x0202) 
{
    WSACleanup ();
    OnCancel();
}

SOCKADDR_IN target;

target.sin_family = AF_INET;
target.sin_port = htons(3124);
target.sin_addr.S_un.S_addr = inet_addr("127.0.0.1");

s = socket ( AF_INET, SOCK_STREAM, IPPROTO_TCP);

if (s == INVALID_SOCKET)
{
    OnCancel();
}

   if (connect(s, (SOCKADDR *)&target, sizeof(target)) == SOCKET_ERROR)
{
    OnCancel();
}
}
