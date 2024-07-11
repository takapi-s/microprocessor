#乗数
M1:     EQU     80H
M2:     EQU     81H

#被乗数
Q1:     EQU     82H
Q2:     EQU     83H

P1:     EQU     84H#部分積
P2:     EQU     85H

n:      EQU     86H

LD      ACC,    00H
ST      ACC,    [P1]
ST      ACC,    [P2]
LD      ACC,    10H
ST      ACC,    [n]

LOOP:   LD      ACC,    [Q1]
        AND     ACC,    01H
        CMP     ACC,    00H
        BZ      SHIFT
        
        LD      ACC,    [P1]
        ADD     ACC,    [M1]
        ST      ACC,    [P1]
        
        BNC     NC
        LD      ACC,    [P2]
        ADD     ACC,    01H
        ST      ACC,    [P2]
        
NC:
        LD      ACC,    [P2]
        ADD     ACC,    [M2]
        ST      ACC,    [P2]
        
        
        
SHIFT:

        LD      ACC,    [M2]
        SLL     ACC
        ST      ACC,    [M2]
        
        LD      ACC,    [M1]
        SLL     ACC
        ST      ACC,    [M1]
        
        BNC     SHIFT2
        LD      ACC,    [M2]
        ADD     ACC,    01H
        ST      ACC,    [M2]
        

SHIFT2:    
        LD      ACC,    [Q1]
        SRL     ACC
        ST      ACC,    [Q1]
        
        LD      ACC,    [Q2]
        SRL     ACC
        ST      ACC,    [Q2]
        
        BNC     ND
        LD      ACC,    [Q1]
        ADD     ACC,    80H
        ST      ACC,    [Q1]
        
        
ND:
        LD      ACC,    [n]
        SUB     ACC,    01H
        ST      ACC,    [n]
        BZ      END
        BA      LOOP
        
END:
        HLT
        END
        
        
        