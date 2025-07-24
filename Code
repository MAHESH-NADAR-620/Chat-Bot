import pyautogui
import time
import pyperclip
from together import Together

client = Together(api_key="")

def is_last_message_from_sender(chat_log, sender_name='Nom Nom Bhai'):
    message = chat_log.split('/2025]')[-1]  # Get the last message
    return sender_name in message

last_processed_message = ""  # Track last Nom Nom Bhai message

pyautogui.click(1130, 1055)  # Focus WhatsApp (or chat window)
time.sleep(2)

while True:
    pyautogui.moveTo(664, 192)
    pyautogui.dragTo(1886, 939, duration=1.0, button='left')
    pyautogui.hotkey('ctrl', 'c')
    pyautogui.click(1127, 1000)
    time.sleep(1)
    chat_history = pyperclip.paste()

    if is_last_message_from_sender(chat_history):
        last_message = chat_history.strip().splitlines()[-1]
        if last_message != last_processed_message:
            print("New message from detected.")
            last_processed_message = last_message  # Update the tracker

            # Generate reply
            completion = client.chat.completions.create(
                model="mistralai/Mixtral-8x7B-Instruct-v0.1",
                messages=[
                    {
                        "role": "system",
                        "content": "You are Mahesh, a fun and witty BE-CSE student from Tamil Nadu studying at Chandigarh University. You speak Hindi, English, and Tamil. Reply casually like a college guy with humor. Only respond if Nom Nom Bhai sent the last message."
                    },
                    {
                        "role": "user",
                        "content": chat_history
                    }
                ]
            )

            response = completion.choices[0].message.content.strip()
            print("Reply:", response)

            pyperclip.copy(response)
            pyautogui.click(1073, 976)  # Focus input field
            pyautogui.hotkey('ctrl', 'v')
            time.sleep(1)
            pyautogui.press('enter')  # Send the message
        else:
            print("Same message already processed. Waiting...")
    else:
        print("Waiting for reply...")

    time.sleep(3)  # Adjust as needed
