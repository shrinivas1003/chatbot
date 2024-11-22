import tkinter as tk
from tkinter import scrolledtext

class BusinessChatbotApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Business Chatbot")
        self.chat_display = scrolledtext.ScrolledText(root, wrap=tk.WORD, state='disabled', width=50, height=20)
        self.chat_display.grid(row=0, column=0, padx=10, pady=10, columnspan=2)
        self.user_input = tk.Entry(root, width=40)
        self.user_input.grid(row=1, column=0, padx=10, pady=10)
        self.user_input.bind("<Return>", self.handle_input)
        self.send_button = tk.Button(root, text="Send", command=self.handle_input)
        self.send_button.grid(row=1, column=1, padx=10, pady=10)

    def append_to_chat(self, sender, message):
        self.chat_display.config(state='normal')
        self.chat_display.insert(tk.END, f"{sender}: {message}\n")
        self.chat_display.config(state='disabled')
        self.chat_display.see(tk.END)

    def handle_input(self, event=None):
        user_message = self.user_input.get().strip()
        if not user_message:
            return
        self.append_to_chat("You", user_message)
        self.user_input.delete(0, tk.END)
        response = self.generate_response(user_message)
        self.append_to_chat("Chatbot", response)

    def generate_response(self, message):
        message = message.lower()
        if "hello" in message or "hi" in message:
            return "Hello! How can I assist you today?"
        elif "how are you" in message:
            return "I'm a chatbot, but I'm doing great! How can I help you?"
        elif "product" in message:
            return "We offer products like A, B, and C. Which one would you like to know more about?"
        elif "price" in message or "pricing" in message:
            return "Our products range from $10 to $500. Please specify the product for detailed pricing."
        elif "support" in message:
            return "For support, please describe your issue, and our team will assist you promptly."
        elif "hours" in message or "business hours" in message:
            return "Our business hours are Monday to Friday, from 9:00 AM to 6:00 PM."
        return "I'm sorry, I didn't understand that. Could you please rephrase?"

if __name__ == "__main__":
    root = tk.Tk()
    app = BusinessChatbotApp(root)
    root.mainloop()
