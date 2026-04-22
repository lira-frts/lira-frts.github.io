# Introdução

Ao decorrer da minha graduação, acredito ter focado mais em matérias de "teoria" e programação competitiva, então resolvi cursar a disciplina de software livre para aprender um pouco mais e sair um pouco da minha zona de conforto. A minha ideia inicial era escrever um blog por semana assim que eu acabasse cada tutorial, mas como eu acabei enrolando, resolvi fazer um único blog para todos os tutoriais.

# Tutoriais

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

# Patch

Ao verificar a lista de sugestões de patches, a que me interessou foi uma que envolvia manipulação de bits (algo que estou levemente acostumado devido programação competitiva) e, ao conversar com a minha dupla (Marcelo Machado Lage), ele também achou interessante.

Então inicialmente, nós tinhamos que:

1- entender as macros que nós iríamos usar (a ideia do patch é alterar umas manipulações de bits que estão sendo feitas de maneira manual/hardcodadas por algumas macros definidas no arquivo include/linux/bitfield.h.).

2- achar algum arquivo que nós pudéssamos alterar, achamos o seguinte: iio/drivers/iio/adc/mcp3422.c.

Após isso, começamos a fazer o patch de fato:

v1 - Inicialmente, nós apenas alteramos algumas macros e alteramos umas manipulações de bits para usar as macros que definidas
em bitfield.h

Porém, esse patch foi recusado pois acabamos fazendo mais de uma coisa em um único commit e, além disso, era possível melhorar o código removendo algumas outras macros que não seriam mais necessárias.

v2 - 1/2: Nesse commit, apenas alteramos algumas macros que estavam definidas (havia mais macros que podiam ser alteradas, mas como elas tinham outros papéis além de manipulação de bits, resolvemos não mexer).

v2 - 2/2: Nesse commit, realizamos as alterações das manipulações de bits que haviam sidos feitas na primeira versão, além disso, removemos as outras macros que haviam sido pedidas.
   
Novamente esse patch foi recusado. A primeira parte devido a ordem que algumas macros estavam definidas (o que eu achei um pouco questionável, pois essa ordem já estava defina: a gente não a alterou no nosso patch) e um comentário que não fazia mais sentido. Já a segunda parte, devido a uma formatação: algumas variáveis deviam estar no definition block (novamente, eu achei questionável pois não haviamos alterado isso em nosso patch).

v3 - 1/2 e 2/2: Arrumamos as sugestões/reclamações feitas acima.

E mais uma vez esse patch foi recusado. A primeira parte devido a mensagem do commit estar errada: a resposta que nos foi dada foi uma revisão feita por um agente de IA que mostrou esse erro e uns outros possíveis erros que já estavam presentes (resolvemos não mexer neles pois pareciam mais avançados para gente). Já segunda parte devido a uma outra alteração que podia ser feita no código (basicamente, usar as macros de manipulação de bits em outro lugar que não estavam sendo usado), o que eu não gostei disso é que essa sugestão podia ser feita facilmente em qualquer outra versão, mas ele (Andy Shevchenko) esperou até aqui para apontar isso.

v4 - ainda vamos fazer...
