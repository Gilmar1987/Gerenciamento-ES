# Gerenciamento-ES 
#Gerenciamento de Entrada e Saída 
#Simulador de Disco

import random

class SimuladorDisco:
    def __init__(self, bloco_minimo, bloco_maximo, posicao_inicial):
        self.bloco_minimo = bloco_minimo
        self.bloco_maximo = bloco_maximo
        self.posicao_atual = posicao_inicial
        self.direcao = 1  # 1 para mover em direção a blocos de números maiores, -1 para menores
        self.fila_requisicoes = []

    def adicionar_requisicao(self, bloco):
        self.fila_requisicoes.append(bloco)

    def scan(self):
        self.fila_requisicoes.sort()
        tempo_total = 0

        while self.fila_requisicoes:
            bloco_mais_proximo = None

            # Encontra a requisição mais próxima na direção atual
            for bloco in self.fila_requisicoes:
                if (self.direcao == 1 and bloco >= self.posicao_atual) or \
                   (self.direcao == -1 and bloco <= self.posicao_atual):
                    if bloco_mais_proximo is None or abs(bloco - self.posicao_atual) < abs(bloco_mais_proximo - self.posicao_atual):
                        bloco_mais_proximo = bloco

            if bloco_mais_proximo is None:
                # Muda de direção se não houver requisição na direção atual
                self.direcao *= -1
                continue

            # Calcula o tempo de busca
            tempo_busca = abs(bloco_mais_proximo - self.posicao_atual)
            tempo_total += tempo_busca

            print(f"Movendo do bloco {self.posicao_atual} para o bloco {bloco_mais_proximo} (Tempo de busca: {tempo_busca})")
            self.posicao_atual = bloco_mais_proximo
            self.fila_requisicoes.remove(bloco_mais_proximo)

        return tempo_total

def main():
    bloco_minimo = int(input("Informe o número mínimo de bloco: "))
    bloco_maximo = int(input("Informe o número máximo de bloco: "))
    posicao_inicial = int(input("Informe a posição inicial da cabeça de disco: "))
    quantidade_requisicoes = int(input("Informe o número de requisições: "))
    
    simulador = SimuladorDisco(bloco_minimo, bloco_maximo, posicao_inicial)
    
    for _ in range(quantidade_requisicoes):
        requisicao = random.randint(bloco_minimo, bloco_maximo)
        simulador.adicionar_requisicao(requisicao)
    
    tempo_total_busca = simulador.scan()
    print(f"Tempo total de busca: {tempo_total_busca}")

if __name__ == "__main__":
    main()





       
  
        
      
        
   
             

   
