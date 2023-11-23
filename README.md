- Robô Yaskawa Motoman
- System Job Captação de dados do Sistema de Visão
<!---
Programa de Captação de dados para o sistema de visão do Robô Yaskawa Motoman
--->
- Legendas
# IN#() - Entrada;
# IG#() - Grupo de entradas (composto por 8 entradas);
 I000 - Variável inteira;
- D000 - Variável double;
- B000 - Variavel booleana;

```
# Necessário no incio de todos os programas
NOP
#Label de identificação do inicio
*INICIO
#Delay para inicio da coleta de dados
DELAY 100
#Espera o sensor da esteira ser acionado (ele trabalha em função reverva, permanecendo ligado até captar algo)
WAIT IN#(1)=OFF
#Recepção dos dados gerados pelo sistema de visão
`RECEBE X ESQUERDO
DIN B001 IG#(21)
DIN B002 IG#(22)
DIN B003 IG#(23)
IF( IG#(24)<>0 ) THEN
  NOT B001 B001
  NOT B002 B002
  NOT B003 B003
ENDIF
`RECEBE Y ESQUERDO
DIN B004 IG#(25)
DIN B005 IG#(26)
DIN B006 IG#(27)
IF( IG#(28)<>0 ) THEN
  NOT B004 B004
  NOT B005 B005
  NOT B006 B006
ENDIF
`RECEBE ANGULO ESQUERDO
DIN B007 IG#(29)
DIN B008 IG#(30)
DIN B009 IG#(31)
IF( IG#(32)<>0 ) THEN
  NOT B007 B007
  NOT B008 B008
  NOT B009 B009
ENDIF
`RECEBE X DIREITO
DIN B021 IG#(33)
DIN B022 IG#(34)
DIN B023 IG#(35)
IF( IG#(36)<>0 ) THEN
  NOT B021 B021
  NOT B022 B022
  NOT B023 B023
ENDIF
`RECEBE Y DIREITO
DIN B024 IG#(37)
DIN B025 IG#(38)
DIN B026 IG#(39)
IF( IG#(40)<>0 ) THEN
  NOT B024 B024
  NOT B025 B025
  NOT B026 B026
ENDIF
`RECEBE ANGULO DIREITO
DIN B027 IG#(41)
DIN B028 IG#(42)
DIN B029 IG#(43)
IF( IG#(44)<>0 ) THEN
  NOT B027 B027
  NOT B028 B028
  NOT B029 B029
ENDIF
`RECEBE IDENTIFICADOR DE LADO
DIN B010 IG#(45)
DIN B011 IG#(46)
DIN B012 IG#(47)
IF( IG#(48)<>0 ) THEN
NOT B010 B010
NOT B011 B011
NOT B012 B012
ENDIF
#Realiza o tratamento dos dados para o inicio do conveyor
`
`
SET D091 B010
SET D092 B011
SET D093 B012
MUL D092 256
MUL D093 65536
ADD D094 D091
ADD D094 D092
ADD D094 D093
#Inicia o processo de conveyor
`Marcador da primeira posição do conveyor
`
`
IF( I010=1 ) THEN
`
`Verifica se é esquerdo
  IF( D094=1000 ) THEN
#Se for reconhecido como esquerdo inicia o processo para as posições do pé esquerdo
`Configura as posições de x
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D001 D091
    ADD D001 D092
    ADD D001 D093
    IF( IG#(24)<>0 ) THEN
      ADD D001 1
      MUL D001 -1
    ENDIF
    `Configura as posições de y
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D002 D091
    ADD D002 D092
    ADD D002 D093
    IF( IG#(28)<>0 ) THEN
      ADD D002 1
      MUL D002 -1
    ENDIF
    `Configura as posições do angulo
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D003 D091
    ADD D003 D092
    ADD D003 D093
    IF( IG#(32)<>0 ) THEN
      ADD D003 1
      MUL D003 -1
    ENDIF
    `Reseta as variaveis
    SET D004 1
    MUL D001 -1
    ADD D002 635000
    ADD D003 0
    MUL D003 10
#Caso não seja esquerda então refaz os processos para as posições do pé direito
    ELSE
`Configura as posições de x
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D001 D091
    ADD D001 D092
    ADD D001 D093
    IF( IG#(36)<>0 ) THEN
      ADD D001 1
      MUL D001 -1
    ENDIF
`Configura as posições de y
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D002 D091
    ADD D002 D092
    ADD D003 D093
    IF( IG#(40)<>0 ) THEN
      ADD D002 1
      MUL D002 -1
    ENDIF
`Configura as posições do angulo
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D003 D091
    ADD D003 D092
    ADD D003 D093
    IF( IG#(44)<>0 ) THEN
      ADD D003 1
      MUL D003 -1
    ENDIF
`Reseta as variáveis
    SET D004 0
    MUL D001 -1
    ADD D002 635000
    ADD D003 0
    MUL D003 10
  ENDIF
ENDIF
#Repete todos os processos para a posição 2 do conveyor
IF( I010=2) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D005 D091
    ADD D005 D092
    ADD D005 D093
    IF( IG#(24)<>0 ) THEN
      ADD D005 1
      MUL D005 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D006 D091
    ADD D006 D092
    ADD D006 D093
    IF( IG#(28)<>0 ) THEN
      ADD D006 1
      MUL D006 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D007 D091
    ADD D007 D092
    ADD D007 D093
    IF( IG#(32)<>0 ) THEN
      ADD D007 1
      MUL D007 -1
    ENDIF
    `
    SET D008 1
    MUL D005 -1
    ADD D006 635000
    ADD D007 0
    MUL D007 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D005 D091
    ADD D005 D092
    ADD D005 D093
    IF( IG#(36)<>0 ) THEN
      ADD D005 1
      MUL D005 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D006 D091
    ADD D006 D092
    ADD D006 D093
    IF( IG#(40)<>0 ) THEN
      ADD D006 1
      MUL D006 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D007 D091
    ADD D007 D092
    ADD D007 D093
    IF( IG#(44)<>0 ) THEN
      ADD D007 1
      MUL D007 -1
    ENDIF
    `
    SET D008 0
    MUL D005 -1
    ADD D006 635000
    ADD D007 0
    MUL D007 10
  ENDIF
ENDIF
IF( I010=3) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D011 D091
    ADD D011 D092
    ADD D0011 D093
    IF( IG#(24)<>0 ) THEN
      ADD D011 1
      MUL D011 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D012 D091
    ADD D012 D092
    ADD D012 D093
    IF( IG#(28)<>0 ) THEN
      ADD D012 1
      MUL D012 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D013 D091
    ADD D013 D092
    ADD D013 D093
    IF( IG#(32)<>0 ) THEN
      ADD D013 1
      MUL D013 -1
    ENDIF
    `
    SET D014 1
    MUL D011 -1
    ADD D012 635000
    ADD D013 0
    MUL D013 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D011 D091
    ADD D011 D092
    ADD D011 D093
    IF( IG#(36)<>0 ) THEN
      ADD D011 1
      MUL D011 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D012 D091
    ADD D012 D092
    ADD D012 D093
    IF( IG#(40)<>0 ) THEN
      ADD D012 1
      MUL D012 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D013 D091
    ADD D013 D092
    ADD D013 D093
    IF( IG#(44)<>0 ) THEN
      ADD D013 1
      MUL D013 -1
    ENDIF
    `
    SET D014 0
    MUL D011 -1
    ADD D012 635000
    ADD D013 0
    MUL D013 10
  ENDIF
ENDIF
IF( I010=4) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D015 D091
    ADD D015 D092
    ADD D015 D093
    IF( IG#(24)<>0 ) THEN
      ADD D015 1
      MUL D015 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D016 D091
    ADD D016 D092
    ADD D016 D093
    IF( IG#(28)<>0 ) THEN
      ADD D016 1
      MUL D016 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D017 D091
    ADD D017 D092
    ADD D017 D093
    IF( IG#(32)<>0 ) THEN
      ADD D017 1
      MUL D017 -1
    ENDIF
    `
    SET D018 1
    MUL D015 -1
    ADD D016 635000
    ADD D017 0
    MUL D017 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D015 D091
    ADD D015 D092
    ADD D015 D093
    IF( IG#(36)<>0 ) THEN
      ADD D015 1
      MUL D015 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D016 D091
    ADD D016 D092
    ADD D016 D093
    IF( IG#(40)<>0 ) THEN
      ADD D016 1
      MUL D016 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D017 D091
    ADD D017 D092
    ADD D017 D093
    IF( IG#(44)<>0 ) THEN
      ADD D017 1
      MUL D017 -1
    ENDIF
    `
    SET D018 0
    MUL D015 -1
    ADD D016 635000
    ADD D017 0
    MUL D017 10
  ENDIF
ENDIF
IF( I010=5) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D021 D091
    ADD D021 D092
    ADD D021 D093
    IF( IG#(24)<>0 ) THEN
      ADD D021 1
      MUL D021 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D022 D091
    ADD D022 D092
    ADD D022 D093
    IF( IG#(28)<>0 ) THEN
      ADD D022 1
      MUL D022 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D023 D091
    ADD D023 D092
    ADD D023 D093
    IF( IG#(32)<>0 ) THEN
      ADD D023 1
      MUL D023 -1
    ENDIF
    `
    SET D024 1
    MUL D021 -1
    ADD D022 635000
    ADD D023 0
    MUL D023 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D021 D091
    ADD D021 D092
    ADD D021 D093
    IF( IG#(36)<>0 ) THEN
      ADD D021 1
      MUL D021 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D022 D091
    ADD D022 D092
    ADD D022 D093
    IF( IG#(40)<>0 ) THEN
      ADD D022 1
      MUL D022 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D023 D091
    ADD D023 D092
    ADD D023 D093
    IF( IG#(44)<>0 ) THEN
      ADD D023 1
      MUL D023 -1
    ENDIF
    `
    SET D024 0
    MUL D021 -1
    ADD D022 635000
    ADD D023 0
    MUL D023 10
  ENDIF
ENDIF
IF( I010=6) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D025 D091
    ADD D025 D092
    ADD D025 D093
    IF( IG#(24)<>0 ) THEN
      ADD D025 1
      MUL D025 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D026 D091
    ADD D026 D092
    ADD D026 D093
    IF( IG#(28)<>0 ) THEN
      ADD D026 1
      MUL D026 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D027 D091
    ADD D027 D092
    ADD D027 D093
    IF( IG#(32)<>0 ) THEN
      ADD D027 1
      MUL D027 -1
    ENDIF
    `
    SET D028 1
    MUL D025 -1
    ADD D026 635000
    ADD D027 0
    MUL D027 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D025 D091
    ADD D025 D092
    ADD D025 D093
    IF( IG#(36)<>0 ) THEN
      ADD D025 1
      MUL D025 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D026 D091
    ADD D026 D092
    ADD D026 D093
    IF( IG#(40)<>0 ) THEN
      ADD D026 1
      MUL D026 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D027 D091
    ADD D027 D092
    ADD D027 D093
    IF( IG#(44)<>0 ) THEN
      ADD D027 1
      MUL D027 -1
    ENDIF
    `
    SET D028 0
    MUL D025 -1
    ADD D026 635000
    ADD D027 0
    MUL D027 10
  ENDIF
ENDIF
IF( I010=7) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D031 D091
    ADD D031 D092
    ADD D031 D093
    IF( IG#(24)<>0 ) THEN
      ADD D031 1
      MUL D031 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D032 D091
    ADD D032 D092
    ADD D032 D093
    IF( IG#(28)<>0 ) THEN
      ADD D032 1
      MUL D032 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D033 D091
    ADD D033 D092
    ADD D033 D093
    IF( IG#(32)<>0 ) THEN
      ADD D033 1
      MUL D033 -1
    ENDIF
    `
    SET D034 1
    MUL D031 -1
    ADD D032 635000
    ADD D033 0
    MUL D033 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D031 D091
    ADD D031 D092
    ADD D031 D093
    IF( IG#(36)<>0 ) THEN
      ADD D031 1
      MUL D031 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D032 D091
    ADD D032 D092
    ADD D032 D093
    IF( IG#(40)<>0 ) THEN
      ADD D032 1
      MUL D032 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D033 D091
    ADD D033 D092
    ADD D033 D093
    IF( IG#(44)<>0 ) THEN
      ADD D033 1
      MUL D033 -1
    ENDIF
    `
    SET D034 0
    MUL D0131 -1
    ADD D032 635000
    ADD D033 0
    MUL D033 10
  ENDIF
ENDIF
IF( I010=8) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D035 D091
    ADD D035 D092
    ADD D035 D093
    IF( IG#(24)<>0 ) THEN
      ADD D035 1
      MUL D035 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D036 D091
    ADD D036 D092
    ADD D036 D093
    IF( IG#(28)<>0 ) THEN
      ADD D036 1
      MUL D036 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D037 D091
    ADD D037 D092
    ADD D037 D093
    IF( IG#(32)<>0 ) THEN
      ADD D037 1
      MUL D037 -1
    ENDIF
    `
    SET D038 1
    MUL D035 -1
    ADD D036 635000
    ADD D037 0
    MUL D037 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D035 D091
    ADD D035 D092
    ADD D035 D093
    IF( IG#(36)<>0 ) THEN
      ADD D035 1
      MUL D035 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D036 D091
    ADD D036 D092
    ADD D036 D093
    IF( IG#(40)<>0 ) THEN
      ADD D036 1
      MUL D036 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D037 D091
    ADD D037 D092
    ADD D037 D093
    IF( IG#(44)<>0 ) THEN
      ADD D037 1
      MUL D037 -1
    ENDIF
    `
    SET D038 0
    MUL D035 -1
    ADD D036 635000
    ADD D037 0
    MUL D037 10
  ENDIF
ENDIF
IF( I010=9) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D041 D091
    ADD D041 D092
    ADD D041 D093
    IF( IG#(24)<>0 ) THEN
      ADD D041 1
      MUL D041 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D042 D091
    ADD D042 D092
    ADD D042 D093
    IF( IG#(28)<>0 ) THEN
      ADD D042 1
      MUL D042 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D043 D091
    ADD D043 D092
    ADD D043 D093
    IF( IG#(32)<>0 ) THEN
      ADD D043 1
      MUL D043 -1
    ENDIF
    `
    SET D044 1
    MUL D041 -1
    ADD D042 635000
    ADD D043 0
    MUL D043 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D041 D091
    ADD D041 D092
    ADD D041 D093
    IF( IG#(36)<>0 ) THEN
      ADD D041 1
      MUL D041 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D042 D091
    ADD D042 D092
    ADD D042 D093
    IF( IG#(40)<>0 ) THEN
      ADD D042 1
      MUL D042 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D043 D091
    ADD D043 D092
    ADD D043 D093
    IF( IG#(44)<>0 ) THEN
      ADD D043 1
      MUL D043 -1
    ENDIF
    `
    SET D044 0
    MUL D041 -1
    ADD D042 635000
    ADD D043 0
    MUL D043 10
  ENDIF
ENDIF
IF( I010=10) THEN
  `
  `
  IF( D094=1000 ) THEN
    SET D094 0
    SET D091 B001
    SET D092 B002
    MUL D092 256
    SET D093 B003
    MUL D093 65536
    ADD D045 D091
    ADD D045 D092
    ADD D045 D093
    IF( IG#(24)<>0 ) THEN
      ADD D045 1
      MUL D045 -1
    ENDIF
    `
    SET D091 B004
    SET D092 B005
    MUL D092 256
    SET D093 B006
    MUL D093 65536
    ADD D046 D091
    ADD D046 D092
    ADD D046 D093
    IF( IG#(28)<>0 ) THEN
      ADD D046 1
      MUL D046 -1
    ENDIF
    `
    SET D091 B007
    SET D092 B008
    MUL D092 256
    SET D093 B009
    MUL D093 65536
    ADD D047 D091
    ADD D047 D092
    ADD D047 D093
    IF( IG#(32)<>0 ) THEN
      ADD D047 1
      MUL D047 -1
    ENDIF
    `
    SET D048 1
    MUL D045 -1
    ADD D046 635000
    ADD D047 0
    MUL D047 10
    ELSE
    SET D094 0
    SET D091 B021
    SET D092 B022
    MUL D092 256
    SET D093 B023
    MUL D093 65536
    ADD D045 D091
    ADD D045 D092
    ADD D045 D093
    IF( IG#(36)<>0 ) THEN
      ADD D045 1
      MUL D045 -1
    ENDIF
    `
    SET D091 B024
    SET D092 B025
    MUL D092 256
    SET D093 B026
    MUL D093 65536
    ADD D046 D091
    ADD D046 D092
    ADD D046 D093
    IF( IG#(40)<>0 ) THEN
      ADD D046 1
      MUL D046 -1
    ENDIF
    `
    SET D091 B027
    SET D092 B028
    MUL D092 256
    SET D093 B029
    MUL D093 65536
    ADD D047 D091
    ADD D047 D092
    ADD D047 D093
    IF( IG#(44)<>0 ) THEN
      ADD D047 1
      MUL D047 -1
    ENDIF
    `
    SET D048 0
    MUL D045 -1
    ADD D046 635000
    ADD D047 0
    MUL D047 10
  ENDIF
ENDIF
#Incrementa a variável I010 em 1
INC I010
#Se o conveyor ultrapassar 10 posições ele volta para a posição 1 e começa a sobrepor as variáveis recebidas
IF( I010>=11 ) THEN
SET IO10 1
ENDIF
#Aguarda a desativação do sensor de esteira
WAIT IN#(1)=ON
#Volta o porgrama para a posição da label inicio
JUMP *INICIO
END
```
