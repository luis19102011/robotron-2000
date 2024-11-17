from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from time import sleep
import sys

# Configurações de Login
EMAIL = "seu_email@example.com"
SENHA = "sua_senha"
MATIFIC_URL = "https://www.matific.com/br/login"

def iniciar_navegador():
    """Inicializa o navegador com o Selenium."""
    options = webdriver.ChromeOptions()
    options.add_argument("--start-maximized")
    return webdriver.Chrome(options=options)

def realizar_login(navegador):
    """Faz o login na plataforma Matific."""
    navegador.get(MATIFIC_URL)
    try:
        # Campo de email
        email_input = WebDriverWait(navegador, 10).until(
            EC.presence_of_element_located((By.ID, "email"))  # Ajustar ID se necessário
        )
        email_input.send_keys(EMAIL)
        
        # Campo de senha
        senha_input = navegador.find_element(By.ID, "password")  # Ajustar ID se necessário
        senha_input.send_keys(SENHA)
        senha_input.send_keys(Keys.RETURN)
        
        print("Login realizado com sucesso!")
    except Exception as e:
        print("Erro ao realizar login:", e)
        navegador.quit()
        sys.exit(1)

def listar_atividades(navegador):
    """Exibe atividades disponíveis (simulado)."""
    print("\nPainel de Atividades:")
    atividades = [
        "Atividade 1: Adição Básica",
        "Atividade 2: Subtração Avançada",
        "Atividade 3: Multiplicação com Frações"
    ]
    for i, atividade in enumerate(atividades, start=1):
        print(f"{i}. {atividade}")
    return atividades

def simular_resolucao(atividades):
    """Simula a resolução das atividades."""
    for i, atividade in enumerate(atividades, start=1):
        print(f"\nIniciando: {atividade}...")
        sleep(2)  # Simula tempo de execução
        print(f"{atividade} concluída com 100% de acerto!")
        print(f"Progresso: {i}/{len(atividades)} concluídas.")

def exibir_painel():
    """Painel principal para gerenciar as atividades."""
    navegador = iniciar_navegador()
    try:
        realizar_login(navegador)
        atividades = listar_atividades(navegador)
        
        print("\nExecutando as atividades...")
        simular_resolucao(atividades)
        
        print("\nTodas as atividades foram concluídas!")
    finally:
        navegador.quit()

if __name__ == "__main__":
    exibir_painel()