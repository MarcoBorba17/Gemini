# Gemini
def main():
  # Inicializa o tabuleiro
  tabuleiro = [[' ', ' ', ' '],
              [' ', ' ', ' '],
              [' ', ' ', ' ']]

  # Define os jogadores
  jogador1 = 'X'
  jogador2 = 'O'

  # Define o jogador inicial
  jogador_atual = jogador1

  # Loop principal do jogo
  while True:
    # Exibe o tabuleiro
    exibir_tabuleiro(tabuleiro)

    # Pede a jogada do jogador atual
    jogada = pedir_jogada(jogador_atual)

    # Verifica se a jogada é válida
    if not jogada_valida(tabuleiro, jogada):
      print("Jogada inválida!")
      continue

    # Marca a jogada no tabuleiro
    marcar_jogada(tabuleiro, jogador_atual, jogada)

    # Verifica se o jogador atual ganhou
    if ganhou(tabuleiro, jogador_atual):
      exibir_tabuleiro(tabuleiro)
      print(f"O jogador {jogador_atual} ganhou!")
      break

    # Troca o jogador atual
    jogador_atual = jogador2 if jogador_atual == jogador1 else jogador1

  # Verifica se o jogo empatou
  if not ganhou(tabuleiro, jogador1) and not ganhou(tabuleiro, jogador2):
    exibir_tabuleiro(tabuleiro)
    print("Empate!")


def exibir_tabuleiro(tabuleiro):
  for linha in tabuleiro:
    print('| ' + ' | '.join(linha) + ' |')


def pedir_jogada(jogador):
  jogada = input(f"Jogador {jogador}, digite sua jogada (1-9): ")
  return int(jogada)


def jogada_valida(tabuleiro, jogada):
  if not 1 <= jogada <= 9:
    return False
  linha = (jogada - 1) // 3
  coluna = (jogada - 1) % 3
  return tabuleiro[linha][coluna] == ' '


def marcar_jogada(tabuleiro, jogador, jogada):
  linha = (jogada - 1) // 3
  coluna = (jogada - 1) % 3
  tabuleiro[linha][coluna] = jogador


def ganhou(tabuleiro, jogador):
  # Verifica linhas
  for linha in tabuleiro:
    if linha[0] == linha[1] == linha[2] == jogador:
      return True

  # Verifica colunas
  for i in range(3):
    if tabuleiro[0][i] == tabuleiro[1][i] == tabuleiro[2][i] == jogador:
      return True

  # Verifica diagonais
  if tabuleiro[0][0] == tabuleiro[1][1] == tabuleiro[2][2] == jogador:
    return True
  if tabuleiro[0][2] == tabuleiro[1][1] == tabuleiro[2][0] == jogador:
    return True

  return False


if __name__ == "__main__":
  main()
