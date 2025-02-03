# SPEECH-RECOGNITION-SYSTEM

*COMPANY*: CODETECH IT SOLUTION

*NAME*: SHARVANI SURAJ MAHADIK

*INTERN ID*:CT08LKR

*DOMAIN*: ARTIFICIAL INTELLIGENCE

*DURATION*:4 WEEKS

*MENTOR*: NEELA SANTOSH

*DESCRIPTION*:

This Python script implements a Speech-to-Text Transcription Tool that converts speech in audio files (WAV or MP3) into text using the following technologies:
speech_recognition: A library used for recognizing speech from an audio file and converting it into text.
gradio: A library used to build the user interface for interacting with the tool. It allows users to upload an audio file and get the transcribed text.
pydub: A library used to handle and manipulate audio files, including converting MP3 files to WAV format.
tempfile: A module used to create temporary files for storing audio data.

Core Functionality:

Transcription Process:
The transcribe_audio function receives an audio file (either a path to a file or a file-like object).
If the file is in MP3 format, it is converted to WAV using the pydub library.
The audio is then processed using the speech_recognition library, which converts the speech in the audio to text using Google’s Speech Recognition API.
The result (either the transcribed text or an error message) is returned.

Gradio Interface:
The gr.Interface function is used to create a simple web interface that allows users to upload audio files (WAV or MP3) and receive transcriptions.
The inputs parameter specifies the input type as an audio file (either WAV or MP3), and outputs specifies that the result should be displayed as text.
A title and description are added to explain the tool’s purpose.
The submit button and background are customized using CSS to provide a lilac background and a purple submit button.

Launching the Tool:
iface.launch(share=True) launches the Gradio interface, which creates a web-based UI that users can interact with to upload audio files and get their transcriptions.

Key Features:
Audio File Input: Users can upload audio files in WAV or MP3 format.
Google Speech Recognition: The transcription process uses Google's powerful Speech-to-Text API.
Customizable UI: The background color and button styles are customized to create a pleasant user experience.
Error Handling: In case of errors (e.g., unrecognized speech or API issues), appropriate error messages are shown.

Importing Libraries:
import speech_recognition as sr
import gradio as gr
from pydub import AudioSegment
import tempfile
import os

Defining the transcribe_audio Function:
def transcribe_audio(audio_file):
    recognizer = sr.Recognizer()
This function takes an audio file as input and processes it using the speech_recognition library.
recognizer = sr.Recognizer() creates an instance of the recognizer that is used to process audio files.

Handling Audio Input:

    try:
        # Check if the audio_file is a file path (string) or an uploaded file object
        if isinstance(audio_file, str):  # It’s a file path
            audio_file_path = audio_file
        else:  # It's a file-like object (gr.Audio gives a file-like object in this case)
            with tempfile.NamedTemporaryFile(delete=False, suffix=".wav") as temp_file:
                # If it's a .mp3 file, convert it to .wav
                if audio_file.name.endswith('.mp3'):
                    sound = AudioSegment.from_mp3(audio_file)
                    sound.export(temp_file.name, format="wav")
                else:
                    temp_file.write(audio_file.read())
                audio_file_path = temp_file.name
This part of the code checks if the input is a file path (string) or a file-like object.
If it’s a file path, the code uses it directly. Otherwise, it creates a temporary file using the tempfile module.
If the uploaded file is an MP3 file, it converts it to WAV using pydub. Otherwise, it saves the audio file directly to the temporary file.

Recognizing Speech from Audio:
    # Load the audio file
        with sr.AudioFile(audio_file_path) as source:
            audio = recognizer.record(source)

        # Use Google Speech Recognition
        text = recognizer.recognize_google(audio)
        return text
with sr.AudioFile(audio_file_path) as source: loads the audio file into the recognizer.
audio = recognizer.record(source) records the audio from the source.
recognizer.recognize_google(audio) uses Google's Speech Recognition API to convert the recorded audio into text.
Error Handling:
    except sr.UnknownValueError:
        return "Sorry, I couldn't understand the audio."
    except sr.RequestError:
        return "There was an issue with the API request."
    except Exception as e:
        return f"An unexpected error occurred: {str(e)}"
If any error occurs during the transcription, such as not being able to understand the audio or API issues, appropriate error messages are returned.

Creating the Gradio Interface:
iface = gr.Interface(
    fn=transcribe_audio, 
    inputs=gr.Audio(type="filepath", label="Upload Audio (WAV or MP3)"),  # Changed to 'filepath'
    outputs="text", 
    live=False,  # Make sure it's not live so users can click submit
    title="Speech-to-Text Transcription Tool",  # Add a title
    description="Upload an audio file (WAV or MP3) and click submit to transcribe it to text.",  # Description
    allow_flagging="never",  # No need to allow flagging
    theme="default",  # Use default theme
    css=""" .gradio-container {background-color: #D8B2D1;}  # Lilac background color
             .gradio-button {background-color: #6A0DAD; color: white;}  # Purple submit button
             .gradio-button:hover {background-color: #8A2BE2;}  # Lighter purple on hover """
)
gr.Interface is used to create the user interface for the app:
fn=transcribe_audio: The function that handles the audio input and returns the transcription.
inputs=gr.Audio(type="filepath", label="Upload Audio (WAV or MP3)"): This input field allows users to upload an audio file (WAV or MP3).
outputs="text": The transcribed text is displayed as the output.
live=False: Makes the interface non-live, meaning users have to click the submit button to start transcription.
title and description: The title and description explain the tool's functionality to the user.
allow_flagging="never": Disables flagging of the results.
theme="default": The default Gradio theme is used for the interface.
css: Custom CSS to set the background color to lilac and make the submit button purple with a hover effect.

Launching the Gradio Interface:
iface.launch(share=True)
This line launches the Gradio app and provides a public link (because of share=True) that anyone can use to interact with the app.
Summary of Functionality:
File Upload: Users can upload an audio file (WAV or MP3).
Speech Recognition: The uploaded audio is converted into text using Google's Speech Recognition API.
Gradio Interface: The tool uses a Gradio interface where users can submit the audio file and view the transcribed text.
UI Customization: The background color is set to lilac, and the submit button is purple with a hover effect.
Result:
When the user uploads an audio file and clicks submit, the audio is processed and transcribed into text. Any errors, such as issues with the audio quality or speech recognition, will return an appropriate message.

*OUTPUT*:

![Image](https://github.com/user-attachments/assets/2059ce9a-5fff-4abb-b960-9508c2e60455)
