# emailkuznetsov-vy_infra
emailkuznetsov-vy Infra repository
bastion_IP = 51.250.7.71
someinternalhost_IP = 10.128.0.24

Комментарии к подключению ко внутреннему хосту:

Для подключения из одно строки сразу к внутреннему хосту можно воспользоваться  тремя способами
1. Через командную строку Proxy:
ssh -o ProxyCommand="ssh -i C:\Users\mails\Desktop\education\ssh\appuser appuser@51.250.7.71 nc %h %p" appuser@10.128.0.24
2. Через ProxyJump:
ssh -i C:\Users\mails\Desktop\education\ssh\appuser -J appuser@51.250.7.71 appuser@10.128.0.24
3.
3.1. добавит в каталог ~/.ssh/ файл конфиг с содержимым:
Host 51.250.7.71
	User appuser

Host someinternalhost
	ProxyJump 51.250.7.71
	User appuser
3.2.подгрузить в ssh-agent (предварительно запустив его) файл с приватным ключем (комманда ssh-add)
3.3.подключиться к внутреннему хосту командой: ssh someinternalhost

P.S. п. 1-2 так же работают без указания пути к приватному ключу если предвариельно загрузить их в ssh-agent команда будет выглядеть:
ssh appuser@51.250.7.71 appuser@10.128.0.24
если добавить еще и файл конфиг из п.3.1, то не нужно будет указывать имя пользователя- команда будет выглядеть:
ssh -J 51.250.7.71 someinternalhost
