link usado = 'https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/ITR/DADOS/'

Bibliotecas usadas

wget: permite realizar o download dos arquivos
pandas: biblioteca que permite realizar as análises
zipfile: usado para elaborar 

#######
#criando um lista com o nome de todos os arquivos, neste caso cria-se uma lista vazia, e cria um loop que irá passar por um range que vai de 2011 a 2020, sendo que o anor está prensente no link da lista
arquivo_zip = []
for ano in range(2011,2021):
    arquivo_zip.append(f'itr_cia_aberta_{ano}.zip')
    
arquivo_zip


########
#realizando o download dos arquivos
for arq in arquivo_zip:
    wget.download(url_base+arq)


########
#Extraindo o arquivo zip, o código "extractall" permite descompactar os arquivos o "()", é a pasta que será criada, no caso, criei um pasta com o nome CVM
for arq in arquivo_zip:
    ZipFile(arq, 'r').extractall('CVM')


########
Este código busca juntar as demonstrações dos anos de 2011 a 2021 em um arquivo apenas csv por demonstração. Neste caso é criado uma lista que passa pelos tipos de demonstrações e junta em arquivo todas informações por ano.

nomes = ['BPA_con', 'BPA_ind', 'BPP_con', 'BPP_ind','DFC_MD_con', 'DFC_MD_ind', 'DFC_MI_con', 'DFC_MI_ind ', 'DMPL_con', 'DMPL_ind','DRE_con','DRE_ind', 'DVA_con', 'DVA_ind']
for nome in nomes:
    arquivo = pd.DataFrame()
    for ano in range(2011,2021):
        arquivo = pd.concat([arquivo, pd.read_csv(f'CVM/itr_cia_aberta_{nome}_{ano}.csv', sep =';', decimal = ',', encoding = 'ISO-8859-1')])
    arquivo.to_csv(f'Dados/itr_cia_aberta_{nome}_2011_2020', index= False)


######

#Filtrando por cnpj 
# Substitua '123456789' pelo CNPJ que você deseja extrair
cnpj_desejado = '56.444.250/0001-75'

# Criando um DataFrame com as informações para o CNPJ desejados
informacoes_cnpj = demonstracao[(demonstracao['CNPJ_CIA'] == cnpj_desejado)]

