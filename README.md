# Introdução

Ao decorrer da minha graduação, acredito ter focado mais em matérias de "teoria" e programação competitiva, então resolvi cursar a disciplina de software livre para aprender um pouco mais e sair um pouco da minha zona de conforto. A minha ideia inicial era escrever um blog por semana assim que eu acabasse cada tutorial, mas como eu acabei enrolando, resolvi fazer um único blog para todos os tutoriais.

## Tutorial 1 - Configuração de ambiente para o desenvolvimento do kernel Linux.

Nesse tutorial, eu comecei a configurar o ambiente de desenvolvimento do Kernel usando o qemu e o libvirt.

Enquanto eu configurava a vm, eu fiz o download de uma imagem "genericcloud" em vez de uma "nocloud", algo que eu só fui perceber quando tentei bootar a vm. Então eu refiz o tutorial de novo baixando a imagem certa (felizmente, isso foi no início do tutorial, então não deu muito trabalho).

Tirando isso, o resto do tutorial foi bem tranquilo de seguir e sem nenhum outro problema. Algo que eu percebi nesse tutorial (e que foi confirmado com os próximos) é que eu não iria absorver (ou entender) tudo que foi falado neles, mas mesmo assim, eu conseguiria entender o básico do que estava acontecendo.

## Tutorial 2 - Configurando, compilando e dando boot em um kernel Linux customizado.

Depois de preparar o ambiente, era hora de mexer no kernel, para isso eu usei o kw.

Semelhante ao último tutorial, esse também foi bem fácil de seguir e felizmente eu não tive nenhum problema (a não ser que eu considere o tempo que kw build demorou pra rodar um problema). 

Por fim, vale destacar que eu não tive a experiência de fazer isso sem o kw, mas acredito que deve ser um processo mais trabalhoso.

## Tutorial 3 e 4 - Modificando o código-fonte do kernel Linux

### Tutorial 3

Agora com o kernel configurado, era hora de mexer com os módulos.

Acredito que esse foi o tutorial que mais me deu dor de cabeça (devido a incompetência minha mesmo): até a parte de buildar a imagem com os módulos (usando o kw build) foi de boas. Porém meus problemas começaram quando eu tentei montar a vm para instalar os módulos, o que dava o seguinte erro: "libguestfs: error: appliance closed the connection unexpectedly", o que eu consegui resolver reiniciando o computador (mais tarde, conversando com meu amigo, ele disse que teve o mesmo erro porque esqueceu de parar a vm, então faz sentido reiniciar também funcionar). Além disso, eu tive problemas com o ssh, pois não estava conseguindo conectar, então eu só fiquei tentando e uma hora foi. E, por fim, na minha primeira tentativa, os módulos não foram carregados, então eu só refiz o tutorial de novo (toda vez que eu executava um kw build tinha vontade de morrer).

Após todo esse sofrimento, eu finalmente consegui. O que eu observei é que talvez se eu tivesse tentado falar com algum monitor antes, eu teria menos dor de cabeça. Porém, acho que esse processo de tentativa e erro fizeram eu ter mais noção do que estava acontecendo (revisando os outros tutoriais).

### Tutorial 4

Ainda mexendo com drives, nesse tutorial eu vi e mexi em character devices devices. Felizmente, após o sofrimento do tutorial 3, esse tutorial foi bem fácil de seguir e não tive nenhum problema :).

## Tutorial 5 e 6 - Preparação para o envio de patches para o kernel Linux

Nesses tutoriais, a ideia era configurar o envio dos patches com email e git.

### Tutorial 5

O tutorial foi mais informativo, uma vez que eu iria usar o email usp que era explicado somente no tutorial 6.

### Tutorial 6

Esse tutorial foi mais aplicado (essa é a palavra certa ?), eu tive que usar o kw e o docker (algo que eu nunca
tinha usado antes!) para configurar o envio de patches pelo email usp.

Esse tutorial, novamente, foi bem fácil de seguir.
