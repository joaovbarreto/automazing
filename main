#Seminário-EngSoftware_Prof.Plotze_202102
#Integrantes e devs do projeto:
#João Victor Barreto 2840481923050
#Victor Castro 2840482113039
#Karlos Eduardo 2840482113041

#Chamada das bibliotecas
from selenium import webdriver
from selenium.webdriver.common.by import By
import pandas as pd
from time import sleep
import pyautogui
import getpass

#Diálogo inicial com o usuário e input dos dados de login
print('\n   >>>>>>>>>> Automazing <<<<<<<<<<   \n\n')
print('Minha função é te auxiliar no cadastro de produtos da plataforma Waymenu! \n')
print('Certifique-se de que exista um arquivo "Produtos.xlsx" em meu diretório, com as colunas:\n')
print('PDV, DESCRIÇÃO, VALOR, GRUPO e MEDIDA, preenchidas com os dados a serem inseridos.\n\n')
print('Agora digite abaixo seus dados de login e deixa que o trabalho é comigo! :)\n')
inputemail = input('E-mail: ')
inputsenha = getpass.getpass('Senha: ')

#Abertura navegador
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])
navegador = webdriver.Chrome(options=options)
navegador.maximize_window()

#Atribuição da função find_element para variável busca
busca = navegador.find_element

#Login na plataforma Waymenu
navegador.get('https://waymenu.com.br/account/login/')
busca(By.XPATH, '//*[@id="formLogin"]/div[1]/input').send_keys(inputemail)
busca(By.XPATH, '//*[@id="formLogin"]/div[2]/input').send_keys(inputsenha)
busca(By.XPATH, '//*[@id="formLogin"]/div[4]/button').click()

# Rotina de cadastro de produtos
tabela = pd.read_excel('Produtos.xlsx') #Processamento da planilha de produtos
sleep(3)
busca(By.XPATH, '//*[@id="accordionSidebar"]/li[3]/a').click()  #btnProdutos
busca(By.XPATH, '//*[@id="collapseProducts"]/div/a[1]').click()  #btnProdutos

for i, pdv in enumerate(tabela["PDV"]):
    valor = tabela.loc[i, "VALOR"]
    descricao = tabela.loc[i, "DESCRIÇÃO"]
    grupo = tabela.loc[i, "GRUPO"]
    medida = tabela.loc[i, "MEDIDA"]
    codigo = tabela.loc[i, "PDV"]

    busca(By.XPATH, '//*[@id="content"]/div/div[1]/div/div[1]/a').click()  #btnNovo
    sleep(1)
    busca(By.XPATH, '//*[@id="createProductForm"]/button').click()  #btnProduto
    busca(By.XPATH, '//*[@id="name"]').send_keys(descricao)  #formDescricao
    busca(By.XPATH, '//*[@id="select2-select-category-container"]').click()  #selecionarGrupo
    busca(By.XPATH, '//*[@id="page-top"]/span/span/span[1]/input').send_keys(grupo)  #formGrupoNome
    pyautogui.press("enter") #formGrupoEnter

    sleep(3)
    busca(By.XPATH, '//*[@id="content"]/div/div[1]/div/div[1]/div/div[2]/button').click()  #btnSalvar
    sleep(5)
    busca(By.XPATH, '//*[@id="price-tab"]').click()  #guiaPreço
    sleep(1)
    busca(By.XPATH, '//*[@id="price-list"]/div/div/div/p/a').click()  # addPreço
    sleep(2)

    busca(By.XPATH, '/html/body/div[1]/div/div/div/div[9]/div/div/div[2]/form/div/div[1]/div/input').send_keys(medida)  #txtUnidade
    busca(By.XPATH, '/html/body/div[1]/div/div/div/div[9]/div/div/div[2]/form/div/div[2]/div/input').send_keys(str(format(valor, ".2f")))  #txtPreço
    busca(By.XPATH, '/html/body/div[1]/div/div/div/div[9]/div/div/div[2]/form/div/div[6]/div/input').send_keys(str(codigo))  #txtPDV
    busca(By.XPATH, '//*[@id="createPriceConfirmationModal"]/div/div/div[3]/button').click()  #btnAdd
    busca(By.XPATH, '//*[@id="content"]/div/div[1]/div/div[1]/div/div[2]/button').click()  #btnSalvar
    busca(By.XPATH, '//*[@id="content"]/div/div[1]/div/div[1]/div/div[1]/form/button').click()  #btnVoltar

print("\nPronto, cadastro de produtos realizado!!!") #MsgFinalConclusão
