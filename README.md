# GPTTALKER
#Description: This Python script allows users to record voice notes using their microphone, transcribe the voice input to text, and receive AI-generated responses using the OpenAI GPT-3.5 language model. Users can have interactive conversations with the AI and receive intelligent replies.
import speech_recognition as sr
import openai

# Set up your OpenAI API key
openai.api_key = 'your OpenAI API key'

# Function to interact with ChatGPT


def chat_with_gpt(prompt):
    response = openai.Completion.create(
        engine='text-davinci-003',  # You can use a different engine if needed
        prompt=prompt,
        max_tokens=50  # Adjust the response length as desired
    )
    return response.choices[0].text.strip()


# Initialize the speech recognizer
recognizer = sr.Recognizer()

while True:
    with sr.Microphone() as source:
        print("Speak something...")
        audio = recognizer.listen(source)

    try:
        text = recognizer.recognize_google(audio)
        if text == "stop":
            print("Stopping the program...")
            break
        print("You said:", text)

        # Pass the transcribed text to ChatGPT
        chat_prompt = f"You said: {text}\n\n"
        gpt_response = chat_with_gpt(chat_prompt)
        print("ChatGPT:", gpt_response)

    except TypeError:
        print("Unable to understand speech")
