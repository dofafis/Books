1. Getting started

- O que é "controle de versão"?
Controle de versão é um sistema que grava as mudanças de um conjunto de arquivos e pastas, de forma que seja possível consultar o histórico dessas alterações e quem as fez. Normalmente é utilizado para versionar código de softwares, mas pode ser usado para qualquer tipo de arquivo de um computador. Um designer por exemplo, pode utilizar um sistema de controle de versão para guardar o histórico de alterações de um layout, imagem e etc.

- Uma pessoa pode utilizar um método manual como controle de versão, uma forma de fazer isso seria é ter várias pastas do projeot em questão e nomeá-los com a data das alterações, mas isso é um método muito suscetível ao erro, pois é fácil esquecer em que pasta está, além de ser difícil de consultar um histórico bem claro de alterações. Por isso programadores desenvolveram VCSs (Version Control Systems) locais com bancos de dados simples para manter o histórico de alterações e gerenciá-las mais facilmente.

- O próximo problema que aparece e precisa ser resolvido em relação a controle de versão, é que normalmente projetos que precisam de um histórico de alterações, tem um time trabalhando no mesmo, o que significa que é preciso manter um registro de alterações geral e um registro de alterações local. Tudo isso começa a ficar complicado demais para lidar manualmente, e precisa contar com um nível de comunicação impecável do time, para que os desenvolvedores não sobreponham as alterações um do outro, não percam históricos de alterações e etc. Para isso forma criados os CVCSs (Centralized Version Control Systems),  ou seja, Sistemas de controle de versão centralizados.

- CVCSs (CVS, Subversion, Perforce), são bem mais fáceis de gerenciar e permite que todos tenham uma visão do que cada um está fazendo, sem precisar lidar com múltiplos bancos na máquina de cada desenvolvedor. O problema é que se o servidor central cair, a colaboração entre os desenvolvedores se torna impossível durante o período, e caso o banco de dados central seja corrompido e não tenha backups apropriados, todo o histórico do projeto é perdido junto. Os sistemas de controle de versão locais sofrem do mesmo problema, pois o histórico está na máquina local e depende da mesma.

- Por isso surgiram os DVCSs (Distributed Version Control Systems). Nesse tipo de sistema, continua existinod um servidor central, mas cada cliente, guarda o repositório completo, ou seja, se o servidor central cair, o histórico não é perdido, pois cada colaborador do projeto tem pode subir novamente o repositório para um novo servidor central, sem perdas, a não ser, claro, que todos os colaborador, tenham apagado seus repositórios locais, mas isso é bem difícil de acontecer.

- O Git é um DVCSs que nasceu da necessidade da comunidade de desenvolvedores do Kernel do Linux de um novo sistema de controle de versão, já que o até então utilizado BitKeeper passou a ser uma ferramenta paga. A partir daí, com a experiência que tiveram utilizando o bitkeeper, a comunidade de desenvolvedores do Kernel Linux, começou a desenvolver sua própria ferramenta. Alguns dos objetivos desse novo sistema seriam:
    - Rápido; 
    - Design simples;
    - Suporte ao desenvolvimento não linear (milhares de ramificações);
    - Completamente distribuído;
    - Capacidade de lidar com grandes projetos como o Kernel do Linux (velocidade e quantidade de dados)

2. O que é o Git?
Diferente dos sistemas de controle de versões, o git não guarda as informações como uma lista de alterações relacionadas aos arquivos. O Git guarda um snapshot/imagem do projeto naquele momento, uma cópia daquele estado do projeto. Caso algum arquivo e/ou pasta não tenha sido alterado em relação ao snapshot anterior do projeto, é guardada apenas uma referência ao arquivo anterior, ganhando eficiência. Sendo assim o Git pensa em seus dados, como uma corrente (stream) de snapshots do projeto.

- Pelo fato de o Git manter uma cópia completa do repositório na máquina local, não é necessário conexão nenhuma para continuar colaborando com o projeto, pode criar sua própria branch, fazer alterações, fazer commit e quando estiver novamente conectado ao repositório remoto, basta dar push. Isso oferece uma velocidade muito maior durante o uso.

- Tudo no git exige uma soma de verificação (checksum), ou seja, não é possível executar qualquer alteração no projeto, sem que o git perceba, mantendo assim a integridade dos dados. O mecanismo usado para esse checksum é SHA-1.

- O Git funciona de forma que basicamente só é possível adicionar informação no banco de dados do Git, ou seja, todo o histórico de tudo, é mantido. Dificilmente você consegue fazer algo que é impossível de desfazer. Ou seja, caso algum erro tenha sido cometido, alterações indesejadas, deleções indesejadas, sempre é possível retornar ao estado anterior do projeto, sem danos, a não ser que o usuário em questão tenha realmente se esforçado para pagar algum histórico permanentemente.

- Existem apenas 3 estados em que qualquer arquivo de um projeto versionado pelo Git pode ser estar, são eles:
    - Modified (Modificado)
    - Staged (Preparado para o próximo commit)
    - Commited (Armazenado permanentemente no histórico de versionamento do Git local)

- Dito isso, existem 3 seções principais do projeto:
    - Working Tree (Árvore de trabalho)
        - É uma área onde uma versão do projeto é retirada da área comprimida do banco de dados na pasta Git para o disco onde você pode modificar os arquivos livremente
    - Staging Area / Index
        - É um arquivo dentro da pasta do Git (Git directory) que guarda informações sobre os arquivos e pastas que serão adicionadas em seu próximo commit
        - Normalmente na terminologia do Git, é chamada de "Index", mas "Staging Area" também está correto
    - Git Directory
        - É a parte mais importante do Git, é onde ele armazena os metadados e o banco de dados orientado a objetos para o seu projeto inteiro. Quando você clona um repositório remoto para sua máquina local, o Git Directory é o que é realmente copiado para sua máquina.

- O fluxo de trabalho utilizando o Git, segue basicamente os seguintes passos:
    - Você modifica os arquivos da árvore de trabalho para consertar algo e/ou adicionar/retirar/melhorar funcionalidades
    - Você escolhe apenas os arquivos relacionado ao seu objetivo principal com aquelas alterações e as coloca na Staging Area
    - Já com os arquivos selecionados e adicionados Staging Area, você faz um commit para registrar permanente essas alterações no Git Directory

3. Command Line (Linha de comando)
    - A forma original e padrão de se usar o Git é pela linha de comando do mesmo. Obviamente já existem várias e várias interfaces gráficas para utilizar o Git de forma mais simples e visualmente agradável, em projetos grandes, essas ferramentas podem ser úteis para visualizar claramente o projeto e para iniciantes, pode ser interessante para ter uma abstração visual do que acontece no Git.
    - Porém, é importante salientar que o único lugar onde é possível executar absolutamente todos os comandos do Git, é na linha de comando, pois as ferramentas gráficas tendem a implementar apenas um subconjunto dos comandos do Git, focando nos mais usados no dia a dia de projetos. Sendo assim, é recomendável saber utilizar o git na linha de comando pois, é a forma padrão e nativa de se usar. Caso se acostume apenas com uma interface gráfica, pode não conseguir utilizar o Git adequadamente em um contexto em que a ferramenta não está disponível. 
    - Lembrando que se sabe mexer na linha de comando, provavelmente saberá mexer pelas interfaces gráficas também

4. 