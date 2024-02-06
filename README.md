# CODSOFT-4 TASK-4
import random
import tkinter as tk
from tkinter import messagebox
class RockPaperScissorsGame:
    def __init__(self, master):
        self.master = master
        self.master.title("Rock Paper Scissors Game")
        self.master.geometry("400x250")
        self.master.configure(bg="#f0f0f0")
        self.user_score = 0
        self.computer_score = 0
        self.user_choice_var = tk.StringVar()
        self.result_var = tk.StringVar()
        self.score_var = tk.StringVar()
        self.create_widgets()
   def create_widgets(self):
        tk.Label(self.master, text="Rock Paper Scissors", font=("Helvetica", 16), bg="#f0f0f0").pack(pady=10)
        choices_frame = tk.Frame(self.master, bg="#f0f0f0")
        choices_frame.pack()

        choices = ['rock', 'paper', 'scissors']
        for choice in choices:
        tk.Radiobutton(choices_frame, text=choice, variable=self.user_choice_var, value=choice, font=("Helvetica", 12), bg="#f0f0f0").pack(side=tk.LEFT, padx=10)

        play_button = tk.Button(self.master, text="Play", command=self.play_game, font=("Helvetica", 12), bg="#4caf50", fg="#ffffff")
        play_button.pack(pady=10)

        result_label = tk.Label(self.master, textvariable=self.result_var, font=("Helvetica", 12), bg="#f0f0f0")
        result_label.pack()

        score_label = tk.Label(self.master, textvariable=self.score_var, font=("Helvetica", 12), bg="#f0f0f0")
        score_label.pack()

        quit_button = tk.Button(self.master, text="Quit", command=self.master.destroy, font=("Helvetica", 12), bg="#ff5733", fg="#ffffff")
        quit_button.pack(pady=10)

    def get_computer_choice(self):
        return random.choice(['rock', 'paper', 'scissors'])

    def determine_winner(self, user_choice, computer_choice):
        if user_choice == computer_choice:
            return 'Tie'
        elif (user_choice == 'rock' and computer_choice == 'scissors') or \
             (user_choice == 'scissors' and computer_choice == 'paper') or \
             (user_choice == 'paper' and computer_choice == 'rock'):
            return 'You Win!'
        else:
            return 'You Lose!'

    def display_result(self, user_choice, computer_choice, result):
        self.result_var.set(f"Your choice: {user_choice}\nComputer's choice: {computer_choice}\nResult: {result}")

    def update_score(self):
        self.score_var.set(f"Score - You: {self.user_score}, Computer: {self.computer_score}")

    def play_game(self):
        user_choice = self.user_choice_var.get()
        computer_choice = self.get_computer_choice()
        result = self.determine_winner(user_choice, computer_choice)
        self.display_result(user_choice, computer_choice, result)

        if result == 'You Win!':
            self.user_score += 1
        elif result == 'You Lose!':
            self.computer_score += 1

        self.update_score()

        if messagebox.askyesno("Play Again", "Do you want to play again?"):
            self.user_choice_var.set('')
            self.result_var.set('')
        else:
            self.master.destroy()
def main():
    root = tk.Tk()
    app = RockPaperScissorsGame(root)
    root.mainloop()

if __name__ == "__main__":
    main()
