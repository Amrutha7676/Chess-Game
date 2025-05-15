# Chess-Game
import chess

def main():
    board = chess.Board()
    print("Welcome to Text-Based Chess!")
    print("Enter your moves in UCI format (e.g., e2e4). Type 'exit' to quit.\n")

    while not board.is_game_over():
        print(board)
        print(f"\nTurn: {'White' if board.turn else 'Black'}")
        move_input = input("Enter your move: ")

        if move_input.lower() == 'exit':
            print("Game exited.")
            break

        try:
            move = chess.Move.from_uci(move_input)
            if move in board.legal_moves:
                board.push(move)
            else:
                print("Illegal move. Try again.\n")
        except ValueError:
            print("Invalid move format. Use UCI format like 'e2e4'.\n")

    if board.is_checkmate():
        print("Checkmate!")
        print(f"{'White' if not board.turn else 'Black'} wins.")
    elif board.is_stalemate():
        print("Stalemate!")
    elif board.is_insufficient_material():
        print("Draw due to insufficient material.")
    elif board.is_seventyfive_moves():
        print("Draw due to the seventy-five-move rule.")
    elif board.is_fivefold_repetition():
        print("Draw due to fivefold repetition.")
    else:
        print("Game over.")

if __name__ == "__main__":
    main()
