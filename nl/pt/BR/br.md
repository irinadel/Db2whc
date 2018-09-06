---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-10"

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
{: shortdesc}

| Plano              | Frequência de backup | Número de backups retidos | Período de retenção de backup   | Autoatendimento |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1/dia          | 2                          | 2 dias; substituição FIFO*   | Não           |
| Flex Performance  | 1/dia          | 7                          | 7 dias; substituição FIFO*   | Sim          |
{: caption="Tabela 1. Frequência e retenção de backup" caption-side="top"}

*Primeiro a entrar, primeiro a sair

## Planos SMP e MPP
{: #smp_mpp}

Os últimos dois backups diários são retidos.

Os backups retidos são usados exclusivamente pela IBM para propósitos de recuperação do sistema somente no caso de um desastre ou perda do sistema. Uma solicitação para restaurar o seu banco de dados por meio de um backup não é suportada. É possível exportar seus dados usando as ferramentas do Db2, como o IBM Data Studio, ou usando o comando **db2
export**. 

## Plano Flex Performance
{: #flex}

As últimas sete capturas instantâneas de backup diário são retidas.

No console do {{site.data.keyword.dashdbshort_notm}}, é possível planejar que seus backups sejam executados quando for mais conveniente e é possível restaurar seu banco de dados por meio de qualquer uma de suas capturas instantâneas de backup retidas em qualquer momento escolhido. O sistema
fica inativo durante o período de restauração. Um e-mail será enviado para notificá-lo de que a operação de restauração foi
concluída.

![Visualização da página de backup e restauração do console da web](images/br.png)

