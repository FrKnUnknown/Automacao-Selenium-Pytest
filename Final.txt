from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import pytest
import time

# Inicializar o driver do Chrome.
driver = webdriver.Chrome()

def test_titulopag1():
    driver.get("https://www.saude.rj.gov.br")
    driver.maximize_window()  # Maximizar janela
    fechar = driver.find_element(By.CLASS_NAME, "close")
    fechar.click()
    time.sleep(3)
    titulo1 = "Saúde RJ"
    # Verifica o titulo da página.
    assert titulo1 == driver.title

def test_buscador():
    # Encontra a caixa de peso/altura e insere os valores
    caixa_pesquisa = driver.find_element(By.NAME, "qw")
    caixa_pesquisa.send_keys("Calcule seu IMC")
    caixa_pesquisa.submit()
    time.sleep(2)
    # Verifica o resultado da seção, se aparece Resultado da Busca.
    resultado_secao = "RESULTADO DA BUSCA"
    assert resultado_secao == driver.find_element(By.CLASS_NAME, "secao-base").text

def test_buscando():
    time.sleep(2)
    resultado_busca = "Saúde RJ - Obesidade - Calcule seu IMC"
    # Verifica o resultado da busca
    assert resultado_busca == driver.find_element(By.CLASS_NAME, "busca-titulo").text
    clique = driver.find_element(By.CLASS_NAME, "busca-titulo")
    clique.click()

def test_titulopag2():
    time.sleep(2)
    titulo2 = "Saúde RJ - Obesidade - Calcule seu IMC"
    # Verifica o titulo da nova página.
    assert titulo2 == driver.title

def test_obesidade():
    obesidade = "OBESIDADE"
    # Verifica a seção base, se contem a palavra Obesidade.
    assert obesidade == driver.find_element(By.CLASS_NAME, "secao-base").text

def test_h1():
    h1eh = "Calcule seu IMC"
    assert h1eh == driver.find_element(By.TAG_NAME, 'h1').text

def test_tema():
    time.sleep(1)
    tema = "CALCULE SEU IMC"
    # Verifica o tema, se contem a palavra Calcule seu IMC.
    assert tema == driver.find_element(By.CLASS_NAME, 'tema').text

def test_imc():
    # Encontra a caixa de peso/altura e insere os valores
    caixa_peso = driver.find_element(By.NAME, "Peso")
    caixa_peso.send_keys('75')
    caixa_altura = driver.find_element(By.NAME, "Altura")
    caixa_altura.send_keys('1,75')
    # Clica no botão de calcular
    time.sleep(3)
    botao_calcular = driver.find_element(By.ID, "Calcular")
    botao_calcular.click()
    time.sleep(3)
    Valor = driver.find_element(By.ID, "Valor").text
    print(Valor)
    Valor = "24,49"
    # Verifica o Resultado/Valor
    assert Valor == driver.find_element(By.ID, "Valor").text

def test_resultado():
    resultado = "RESULTADO"
    # Verifica se a nova pagina apresenta a palavra Resultado
    assert resultado == driver.find_element(By.XPATH, '//*[@id="Resposta"]/div[1]').text

def test_refazer():
    refazer_calculo = "REFAZER CÁLCULO"
    # Verifica se a nova pagina apresenta a palavra Refazer cálculo
    assert refazer_calculo == driver.find_element(By.XPATH, '//*[@id="Resposta"]/div[2]/a').text
    time.sleep(1)
    botao_refazer = driver.find_element(By.XPATH, '//*[@id="Resposta"]/div[2]/a')
    botao_refazer.click()
    time.sleep(3)
    driver.quit()