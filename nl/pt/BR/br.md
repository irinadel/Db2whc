---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Backup e restauração
{: #br}

Um backup criptografado no banco de dados {{site.data.keyword.dashdbshort_notm}} integral é feito uma vez por
dia. 
Para o plano Flex Performance, as capturas instantâneas dos sete últimos backups diários são retidas. Para os planos SMP e MPP, os
últimos dois backups diários são retidos.
{: shortdesc}

No plano Flex Performance, é possível planejar seus backups para serem executados quando for mais conveniente e é possível restaurar
seu banco de dados de qualquer uma de suas capturas instantâneas de backup retidas em qualquer momento que você escolher. O sistema
fica inativo durante o período de restauração. Um e-mail será enviado para notificá-lo de que a operação de restauração foi
concluída.

No caso dos planos SMP e MPP, os backups retidos são usados exclusivamente pela IBM apenas para fins de recuperação do sistema no caso de um desastre ou de uma perda do sistema. Uma solicitação para restaurar o seu banco de dados por meio de um backup não é suportada. É possível exportar seus dados usando as ferramentas do Db2, como o IBM Data Studio, ou usando o comando **db2
export**. 
