#Partes usadas no trabalho (Clicar no nome do arquivo README e colocar em modo CODE no canto superior esquerdo da aba)

#Leitura da Planilha e renomendo colunas

import pandas as pd
import matplotlib.pyplot as plt
lista = pd.read_csv('database_grupo3.csv')

lista = lista.rename(columns={lista.columns[0]:'Gender'})
lista = lista.rename(columns={lista.columns[1]:'Race/Ethnicity'})
lista = lista.rename(columns={lista.columns[2]:'P.L.E.'}) #Parental Level of Education
lista = lista.rename(columns={lista.columns[3]:'Lunch'})
lista = lista.rename(columns={lista.columns[4]:'Preparation'})
lista = lista.rename(columns={lista.columns[5]:'Math'})
lista = lista.rename(columns={lista.columns[6]:'Reading'})
lista = lista.rename(columns={lista.columns[7]:'Writing'})

#Separação do database por grupos, gênero, escolaridade dos pais e refeição em diferentes listas

groupA=lista.loc[lista['Race/Ethnicity']=='group A']
groupB=lista.loc[lista['Race/Ethnicity']=='group B']
groupC=lista.loc[lista['Race/Ethnicity']=='group C']
groupD=lista.loc[lista['Race/Ethnicity']=='group D']
groupE=lista.loc[lista['Race/Ethnicity']=='group E']
Female=lista.loc[lista['Gender']=='female']
Male=lista.loc[lista['Gender']=='male']
Some=lista.loc[lista['P.L.E.']=='some college']
Associate=lista.loc[lista['P.L.E.']=="associate's degree"]
High=lista.loc[lista['P.L.E.']=='high school']
Bachelor=lista.loc[lista['P.L.E.']=="bachelor's degree"]
Master=lista.loc[lista['P.L.E.']=="master's degree"]
SomeHigh=lista.loc[lista['P.L.E.']=="some high school"]
Standard=lista.loc[lista['Lunch']=='standard']
Free=lista.loc[lista['Lunch']=='free/reduced']
Completed=lista.loc[lista['Preparation']=='completed']
Non=lista.loc[lista['Preparation']=='none']
#Resetando o Index dos novos grupos
groupA= groupA.reset_index()
groupB= groupB.reset_index()
groupC= groupC.reset_index()
groupD= groupD.reset_index()
groupE= groupE.reset_index()
Female=Female.reset_index()
Male=Male.reset_index()
Some=Some.reset_index()
Associate=Associate.reset_index()
High=High.reset_index()
Bachelor=Bachelor.reset_index()
Master=Master.reset_index()
SomeHigh=SomeHigh.reset_index()
Free=Free.reset_index()
Standard=Standard.reset_index()
Completed=Completed.reset_index()
Non=Non.reset_index()

#Transformando dataframes para listas

groupALM=groupA['Math'].tolist()
groupBLM=groupB['Math'].tolist()
groupCLM=groupC['Math'].tolist()
groupDLM=groupD['Math'].tolist()
groupELM=groupE['Math'].tolist()
groupALR=groupA['Reading'].tolist()
groupBLR=groupB['Reading'].tolist()
groupCLR=groupC['Reading'].tolist()
groupDLR=groupD['Reading'].tolist()
groupELR=groupE['Reading'].tolist()
groupALW=groupA['Writing'].tolist()
groupBLW=groupB['Writing'].tolist()
groupCLW=groupC['Writing'].tolist()
groupDLW=groupD['Writing'].tolist()
groupELW=groupE['Writing'].tolist()
femaleLM=Female['Math'].tolist()
femaleLR=Female['Reading'].tolist()
femaleLW=Female['Writing'].tolist()
maleLM=Male['Math'].tolist()
maleLR=Male['Reading'].tolist()
maleLW=Male['Writing'].tolist()
someLM=Some['Math'].tolist()
someLR=Some['Reading'].tolist()
someLW=Some['Writing'].tolist()
associateLM=Associate['Math'].tolist()
associateLR=Associate['Reading'].tolist()
associateLW=Associate['Writing'].tolist()
highLM=High['Math'].tolist()
highLR=High['Reading'].tolist()
highLW=High['Writing'].tolist()
bachelorLM=Bachelor['Math'].tolist()
bachelorLR=Bachelor['Reading'].tolist()
bachelorLW=Bachelor['Writing'].tolist()
masterLM=Master['Math'].tolist()
masterLR=Master['Reading'].tolist()
masterLW=Master['Writing'].tolist()
somehighLM=SomeHigh['Math'].tolist()
somehighLR=SomeHigh['Reading'].tolist()
somehighLW=SomeHigh['Writing'].tolist()
freeLM=Free['Math'].tolist()
freeLR=Free['Reading'].tolist()
freeLW=Free['Writing'].tolist()
standardLM=Standard['Math'].tolist()
standardLR=Standard['Reading'].tolist()
standardLW=Standard['Writing'].tolist()
completedLM=Completed['Math'].tolist()
completedLR=Completed['Reading'].tolist()
completedLW=Completed['Writing'].tolist()
nonLM=Non['Math'].tolist()
nonLR=Non['Reading'].tolist()
nonLW=Non['Writing'].tolist()

#Cálculo de média,variância e desvio padrão geral

print('==============NOTAS GERAIS==============')
geralnotas=[MathL,ReadL,WriteL]
grupoGeral=['Math','Reading','Writing']
GeralSum=[0,0,0,0,0,0]
GeralMedia=[0,0,0,0,0,0]
GeralSoma=[0,0,0,0,0,0]
GeralSoma2=[0,0,0,0,0,0]
GeralVar=[0,0,0,0,0,0]
GeralDesvio=[0,0,0,0,0,0]
#Somatório e médias
for i in range (len(geralnotas)):
    for j in range (len(geralnotas[i])):
        GeralSum[i]=geralnotas[i][j]+GeralSum[i]
    GeralMedia[i]=GeralSum[i]/(len(geralnotas[i]))
#Somatórios(x-media)^2, Variância e Desvios
for i in range (len(geralnotas)):
    for j in range (len(geralnotas[i])):
        GeralSoma[i]=geralnotas[i][j]-GeralMedia[i]
        GeralSoma2[i]=pow(GeralSoma[i],2.0)+GeralSoma2[i]
    GeralVar[i]=GeralSoma2[i]/(len(geralnotas[i]))
    GeralDesvio[i]=pow(GeralVar[i],0.5)
print('---------------Math--------------------------------------')
for i in range (len(geralnotas)):
    print("Subject: {} ==>\nSomatório: [{}]  Média: [{}]  Variância: [{}]  Desvio Padrão: [{}]\n".format(grupoGeral[i],GeralSum[i],round(GeralMedia[i],5),round(GeralVar[i],5),round(GeralDesvio[i],5)))

#Porcentagem de homens e mulheres por grupo de A-E

femA,femB,femC,femD,femE,malA,malB,malC,malD,malE=0,0,0,0,0,0,0,0,0,0
listagroup = [groupA,groupB,groupC,groupD,groupE]
listagenderf= [femA,femB,femC,femD,femE]
listagenderm=[malA,malB,malC,malD,malE]
percfemale = [0,0,0,0,0,0]
percmale= [0,0,0,0,0,0]	
femScore =[femaleLM,femaleLR,femaleLW]
malScore= [maleLM,maleLR,maleLW]
gruposgenerof=[]
gruposgenerom=[]
for i in range (len(listagroup)):
    listagenderf[i] = listagroup[i].loc[listagroup[i]['Gender']=='female']
    listagenderm[i] = listagroup[i].loc[listagroup[i]['Gender']=='male']
for i in range (5):
    percfemale[i]=(len(listagenderf[i])*100)/(len(listagroup[i]))
    percmale[i]=len(listagenderm[i])*100/len(listagroup[i])
for i in range (5):
    print("Group {}: Male= {}%\n         Female= {}%\n".format(grupos[i],round(percmale[i],5),round(percfemale[i],5)))
    
#Porcentagem de alimentação Standard e Free por grupo de A-E

lunchgroup=[0,0,0,0,0]
lunchperc=[0,0,0,0,0]
freelunchgroup=[0,0,0,0,0]
freelunchperc=[0,0,0,0,0]
print('Alimentação Standard Total     Alimentação Free/Reduced Total')
for i in range (len(listagroup)):
    lunchgroup[i]=listagroup[i].loc[listagroup[i]['Lunch']=='standard']
    lunchperc[i]=len(lunchgroup[i])/(len(standardLM))*100
    freelunchgroup[i]=listagroup[i].loc[listagroup[i]['Lunch']=='free/reduced']
    freelunchperc[i]=len(freelunchgroup[i])/(len(freeLR))*100
for i in range (len(grupos)):
    print('\nGrupo: {}: {}%             Grupo:{}: {}%'.format(grupos[i],round(lunchperc[i],5),grupos[i],round(freelunchperc[i],5)))
    
#Porcentagem de alunos com preparação completa por grupo de A-E

prepgroup=[0,0,0,0,0]
prepperc=[0,0,0,0,0]
print('Porcentagem de alunos com preparação completa por grupo')
for i in range (len(prepgroup)):
    prepgroup[i] = listagroup[i].loc[listagroup[i]['Preparation']=='completed']
    prepperc[i]= len(prepgroup[i])/(len(listagroup[i]))*100
for i in range (len(prepperc)):
    print('\nGrupo {}: {}%'.format(grupos[i],round(prepperc[i],5)))
    
#Quartil MATH

Q1= int(len(MathL)/4)
Q2= int(len(MathL)/4*2)
Q3= int(len(MathL)/4*3)
Quartis = [Q1,Q2,Q3]
QMath=[0,0,0]
for i in range(len(Quartis)):
    QMath[i]=MathL[Quartis[i]]
QMath
DIM=(QMath[2]-QMath[0])
LIM=QMath[0]-1.5*DIM
LSM=QMath[2]+1.5*DIM
print('=============MATH=============\nQuartis= {}\nLimite Inferior= {}\nLimite Superior= {}\n'.format(QMath,LIM,LSM))

#Quartil Read

ReadL=lista['Reading'].tolist()
ReadL.sort()
QRead=[0,0,0]
for i in range(len(Quartis)):
    QRead[i]=ReadL[Quartis[i]]
DIR=(QRead[2]-QRead[0])
LIR=QRead[0]-1.5*DIR
LSR=QRead[2]+1.5*DIR
print('=============READ=============\nQuartis= {}\nLimite Inferior= {}\nLimite Superior= {}'.format(QRead,LIR,LSR))

#Quartil Write

WriteL=lista['Writing'].tolist()
WriteL.sort()
QWrite=[0,0,0]
for i in range(len(Quartis)):
    QWrite[i]=WriteL[Quartis[i]]
DIW=(QWrite[2]-QWrite[0])
LIW=QWrite[0]-1.5*DIW
LSW=QWrite[2]+1.5*DIW
print('=============WRITE=============\nQuartis= {}\nLimite Inferior= {}\nLimite Superior= {}'.format(QWrite,round(LIW),round(LSW)))
