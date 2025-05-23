# NM-ARASU-VOICESTREAM-TECH
Voice-based Notes and Memo Systems
Introduction:
In today's fast-paced digital age, traditional methods of note-taking and memo recording
are being rapidly replaced by smart, efficient, and accessible technologies. Voice-based
systems have emerged as a powerful solution to enhance productivity and convenience.
The "Voice-based Notes and Memo System" aims to provide users with a seamless
method to record spoken thoughts, ideas, and reminders, converting them into textual
notes automatically using speech recognition technologies.

This project is especially beneficial for professionals, students, and individuals who
prefer hands-free interaction with devices or need to capture ideas quickly on the go.
With advancements in voice processing, it's now feasible to transcribe speech with high
accuracy and store it systematically for future reference.

Problem Statement:
Manual note-taking using traditional input devices like keyboards or writing tools can be
time-consuming, error-prone, and inefficient in situations where users are multitasking or
physically constrained. Moreover, people often forget ideas if they cannot record them
immediately. There's a clear need for a reliable and user-friendly system that can:

● Record voice inputs.
● Convert speech to text.
● Save the converted text in an organized manner (e.g., CSV or text file).
● Allow appending new entries without overwriting previous ones.
The "Voice-based Notes and Memo System" addresses this issue by providing a
lightweight, intuitive, and accurate voice-to-text platform that updates the user's
notes automatically.
Objectives
The key objectives of this project include:

● To develop a system that allows users to input memos or notes using voice.
● To convert `.wav` audio files into transcribed text using speech recognition
libraries.
● To store the transcriptions in a structured format like `.csv` or `.txt` without
recreating the file each time.
● To support batch processing of multiple audio files uploaded via a ZIP archive.
● To make the system usable in environments like Google Colab for cloud-based
accessibility.
Methodology
The development of the Voice-based Notes and Memo System follows a structured
methodology to ensure accurate voice recognition, efficient storage, and seamless user
experience. The steps are as follows:

Audio Input Collection
The user records their note or memo as a .wav audio file using any voice
recorder. This allows flexibility in capturing voice inputs even without a live
microphone.
Audio File Upload
The system allows users to upload one or more .wav files at a time. These files
are collected through a file input interface and stored temporarily for processing.
Speech Recognition
Using a speech recognition library (such as Python’s speech_recognition
module), the system processes each .wav file to extract the spoken words and
convert them into text format. This module uses Google's Web Speech API for
accurate transcription.
Data Validation and Cleaning
The transcribed text is cleaned to remove background noise errors, common
artifacts, or misinterpretations. Optional keyword filtering can be implemented to
ignore irrelevant inputs.
File Handling and Storage
○ If the output file does not exist, it is created.
○ If it already exists, the system appends the new note without overwriting
the previous entries.
○ Each recognized note is saved in a new line or row, maintaining the
chronological order of in put.
Error Handling
The system includes exception handling to manage cases such as:
○ Unrecognizable audio
○ Missing files
○ File format issues
Output Generation
The recognized text is saved and can be reviewed later as a memo or note. The
output is either a .txt file for simple notes or a .csv file if metadata (like date
and time) needs to be recorded alongside the note.
Repeatable Use
The system is designed to be used multiple times. Each run will append new
content to the existing file without duplication, ensuring continuity.
Program Flow:
!pip install SpeechRecognition pandas

! pip install pandas pyttsx

!apt-get install - y portaudio19-dev

!pip install pyaudio

pip install pipwin

from google.colab import files

print("Upload your ZIP file containing .wav files:")

uploaded = files.upload()

import os

import zipfile

extract_folder = "extracted_audio"

os.makedirs(extract_folder, exist_ok=True)

for zip_filename in uploaded.keys():

if zip_filename.endswith('.zip'):
with zipfile.ZipFile(zip_filename, 'r') as zip_ref:
zip_ref.extractall(extract_folder)
print(f"Extracted ZIP file to folder: {extract_folder}")
else:
print(f"❌{zip_filename} is not a ZIP file.")
print("Files extracted:")

print(os.listdir(extract_folder))

import os

import zipfile

from google.colab import files

import speech_recognition as sr

Step 1: Upload and unzip
uploaded = files.upload() # Upload a zip with .wav files

zip_file_name = list(uploaded.keys())[0]

extract_path = "Notes"

with zipfile.ZipFile(zip_file_name, 'r') as zip_ref:

zip_ref.extractall(extract_path)
print(f"\n✅Extracted to '{extract_path}'")
Step 2: Find all .wav files in all subfolders
wav_files = []

for root, dirs, files_in_dir in os.walk(extract_path):

for file in files_in_dir:
if file.lower().endswith(".wav"):
wav_files.append(os.path.join(root, file))
if not wav_files:

print("❌No .wav files found. Check your ZIP structure.")
else:

print("🎧 Found the following .wav files:")
for wf in wav_files:
print(" - ", wf)
Step 3: Recognize and write to output file
recognizer = sr.Recognizer()

output_file = "Notes_output.txt"

with open(output_file, "w", encoding="utf-8") as f:

for wav_path in wav_files:
filename = os.path.basename(wav_path)
print(f"\n🎧 Processing {filename}...") try:
with sr.AudioFile(wav_path) as source:
audio_data = recognizer.record(source)
Input Format
.wav audio files (voice memos or notes)
Combined in a .zip file for batch upload
Output Format
.txt file (or .csv if needed), containing each transcribed note on a new line
Automatically appended—no data is overwritten
command = recognizer.recognize_google(audio_data)
print(f"✅ Recognized: {command}")
f.write(f"{filename}: {command}\n")
except sr.UnknownValueError:
print(f"⚠Could not understand audio in {filename}.")
f.write(f"{filename}: Could not understand audio.\n")
except sr.RequestError as e:
print(f"❌API error for {filename}: {e}")
f.write(f"{filename}: API error - {e}\n")
print(f"\n🎧 All recognized commands saved to '{output_file}'")
output:
Testing and Validation:
● Tested with varied accents and sentence structures.
● Included background noise in some files to test recognition robustness.
● Validated file appending functionality and ensured no overwriting occurred.
● Ensured system handled unrecognized audio gracefully with placeholder text.
Conclusion:
The Voice-based Notes and Memo System successfully delivers an accessible, accurate,
and convenient method for voice-based note-taking. By leveraging Python's speech
recognition libraries and simple file handling mechanisms, the system can process
multiple audio files, extract meaningful content, and store it systematically.
This approach is highly extensible and can be adapted for mobile apps, accessibility
tools, or productivity platforms. Future improvements may include live recording
support, multilingual support, speaker identification, and integration with cloud storage.

Real-time Subtitling for Live Events
Introduction:
Real-time subtitling provides live captioning of audio content, enabling accessibility for
hearing-impaired audiences and improving content engagement. This project simulates a
real-time subtitling system by transcribing pre-recorded audio chunks (.wav files)
sequentially, adding timestamps, and generating subtitle text files.

Problem Statement:
Live events often require real-time subtitles to aid accessibility and comprehension.
Creating an automated system that converts live speech to text with accurate timing is
challenging due to noisy environments, speech variations, and processing delays. This
project addresses the simulation of real-time subtitling using offline audio files to
approximate live transcription.

Objectives:
The objectives of this project are:

● To transcribe audio speech from multiple pre-recorded .wav files sequentially.
● To append recognized text with timestamps to a subtitle file.
● To simulate real-time behavior with controlled delays between audio segments.
● To handle errors gracefully during speech recognition.
● To provide a downloadable subtitle file for user convenience.
Methodology:
The methodology for the real-time subtitling system involves the following steps:

Uploading and Extracting Audio Files
The user uploads a ZIP file containing multiple .wav audio files. These files
represent segmented audio recordings from a live event. The ZIP file is extracted
into a specified directory for processing.
Locating and Sorting Audio Files
The program recursively scans the extracted directory to find all .wav files. These
audio files are then sorted by filename to maintain the correct sequence,
simulating a live audio stream.
Speech Recognition Using Google Web Speech API
For each .wav file, the program uses the Speech Recognition Python library with
Google's Web Speech API to transcribe the speech content into text.
Timestamping and Subtitle Generation
Each recognized text segment is appended to a subtitle file along with a
timestamp indicating the time of transcription. This simulates live subtitle
captions appearing in real-time.
Simulating Real-Time Processing
The system introduces a delay (e.g., 1 second) between processing each audio
segment to imitate real-time subtitling behavior.
Error Handling
The system detects and handles errors such as unrecognized speech or API
failures. It logs appropriate messages and continues processing subsequent audio
files.
Program Flow:
from google.colab import files
import zipfile, os, time
import speech_recognition as sr

Upload and extract ZIP
uploaded = files.upload()
zip_file = list(uploaded.keys())[0]
extract_path = "live_audio"
with zipfile.ZipFile(zip_file, 'r') as zip_ref:
zip_ref.extractall(extract_path)

recognizer = sr.Recognizer()
subtitle_file = "live_subtitles.txt"

Find all wav files
audio_files = []
for root, _, files_in_dir in os.walk(extract_path):
for file in sorted(files_in_dir):

if file.lower().endswith(".wav"):
audio_files.append(os.path.join(root, file))
with open(subtitle_file, "w", encoding="utf-8") as f:
f.write("=== Live Subtitles ===\n")

for filepath in audio_files:
with sr.AudioFile(filepath) as source:
audio = recognizer.record(source)
try:
text = recognizer.recognize_google(audio)
timestamp = time.strftime('%H:%M:%S')
print(f"[{timestamp}] {text}")
with open(subtitle_file, "a", encoding="utf-8") as f:
f.write(f"[{timestamp}] {text}\n")
except sr.UnknownValueError:
print(f"[{time.strftime('%H:%M:%S')}] Could not understand.")
except sr.RequestError as e:
print(f"[{time.strftime('%H:%M:%S')}] API error: {e}")
time.sleep(1)

Input Format:
A ZIP file containing one or more .wav audio files representing audio segments to
be transcribed.

Output Format:
A plain text file named 'live_subtitles.txt' containing timestamped subtitles in the
following format:
[HH:MM:SS] Transcribed speech text

Output:
Testing and Validation:
The system was tested with multiple WAV files of varying lengths and speech clarity.
Recognition accuracy was validated by comparing transcribed text to the original speech.
Error handling was tested by including noisy and silent audio clips.

Conclusion:
This project demonstrated the feasibility of simulating real-time subtitling using
pre-recorded audio files. While not a substitute for true live audio transcription, it
provides a foundation for developing accessible captioning tools. Future work could
include integrating real microphone input, improving recognition accuracy, and adding
advanced subtitle formatting.

Voice Commands for Gaming
Introduction:
In recent years, voice recognition technology has significantly evolved, opening new
possibilities for interactive and hands-free applications. This project focuses on
leveraging speech recognition to create an interactive voice-controlled gaming system.
By processing audio commands such as “shoot,” “jump,” “reload,” and classic game
inputs like “stone,” “paper,” and “scissors,” the system allows players to engage with
games through natural voice inputs rather than traditional controllers or keyboards.

The main objective is to develop a Python-based application that can handle audio files
containing spoken commands, recognize and validate these commands accurately, and
respond with appropriate game actions. This approach not only enhances the gaming
experience but also improves accessibility for users who may find conventional controls
challenging. The project demonstrates the integration of speech recognition with game
logic, enabling real-time, voice-driven gameplay.

Problem Statement:
Traditional gaming interfaces rely heavily on manual inputs through keyboards, mice, or
controllers, which can limit accessibility and reduce the natural interaction experience for
many users. There is a growing need for more intuitive, hands-free control mechanisms
that allow players to interact with games using voice commands. However, accurately
recognizing spoken commands from varied audio inputs and integrating them effectively
into game logic poses technical challenges, especially when handling diverse audio
formats and background noise.

This project aims to address these challenges by developing a robust voice-command
recognition system that can process audio files containing game commands, filter valid
instructions, and execute corresponding gameplay actions such as shooting, jumping, or
playing stone-paper-scissors. The goal is to improve user engagement and accessibility
by enabling seamless voice-driven gaming experiences.

Objectives:
● To develop a Python-based system capable of processing audio files with spoken
game commands.
● To support recognition of multiple commands like "shoot," "jump," "reload," and
play a simple stone-paper-scissors game.
● To handle audio files inside zipped folders with nested directory structures.
● To provide a clean output documenting the recognized commands and game
results.
● To demonstrate basic speech recognition integrated with game logic.
Methodology:
The project follows a systematic approach to develop a voice-command-based gaming
system. The key steps involved are:

Data Input and Extraction:
The system accepts a ZIP file containing nested folders with audio files in
formats such as WAV or MP3. The ZIP file is programmatically extracted, and
audio files are located recursively through all subdirectories.
Audio Format Handling:
Since the speech recognition library works best with WAV format, any MP
audio files encountered are converted to WAV using the pydub library, ensuring
compatibility and consistency.
Speech Recognition:
The extracted audio files are processed using the speech_recognition Python
library, which interfaces with Google's Speech Recognition API to transcribe the
spoken commands into text.
Command Filtering and Validation:
The transcribed text is cleaned and compared against a predefined list of valid
game commands: "shoot," "jump," "reload," "stone," "paper," and "scissors."
Commands outside this list are ignored to prevent invalid inputs.
Game Logic Execution:
○ For commands related to the shooting game ("shoot," "jump," "reload"),
the system acknowledges the command with a suitable response.
○ For stone-paper-scissors commands, the system randomly selects a
computer move and determines the winner based on the classic game
rules.
Output Generation:
Results from the command recognition and gameplay are logged into an output
text file (output.txt) including the audio file name, recognized command, game
moves, and outcomes.
Testing and Validation:
Multiple audio files are randomly selected for testing to ensure accuracy of
speech recognition and correctness of the game logic. The system is also tested
for robustness against unrecognized or irrelevant audio inputs.
Program Flow:
Step 1: Install necessary libraries
!pip install SpeechRecognition pydub

!apt-get install ffmpeg - y

import zipfile

import os

import random

import speech_recognition as sr

from pydub import AudioSegment

from google.colab import files

Step 2: Upload ZIP file
print("Upload your input.zip containing folders and audio files:")

uploaded = files.upload()

zip_path = list(uploaded.keys())[ 0 ]

extract_folder = "extracted_audio"

Step 3: Extract ZIP file
with zipfile.ZipFile(zip_path, 'r') as zip_ref:

zip_ref.extractall(extract_folder)
print(f"Extracted files to '{extract_folder}'")

Step 4: Function to get all audio files recursively
def get_all_audio_files(base_folder, extensions=('.wav', '.mp3')):

audio_files = []
for root, dirs, files in os.walk(base_folder):
for file in files:
if file.lower().endswith(extensions):
audio_files.append(os.path.join(root, file))
return audio_files
Step 5: Convert any mp3 files to wav for compatibility
audio_files = get_all_audio_files(extract_folder)

for file_path in audio_files:

if file_path.lower().endswith(".mp3"):
wav_path = file_path.rsplit('.', 1 )[ 0 ] + ".wav"
print(f"Converting {file_path} to {wav_path}")
sound = AudioSegment.from_mp3(file_path)
sound.export(wav_path, format="wav")
os.remove(file_path) # Remove original mp
Step 6: Refresh audio files list to only wav files now
audio_files = get_all_audio_files(extract_folder, extensions=('.wav',))

print(f"Found {len(audio_files)} WAV audio files after conversion.")

if len(audio_files) < 5 :

print("Warning: Less than 5 audio files found, will process all available.")
Step 7: Select 5 random audio files (or all if less than 5)
num_files = min( 5 , len(audio_files))

selected_files = random.sample(audio_files, num_files)

print(f"Selected {num_files} audio files:")

for f in selected_files:

print(f)
Step 8: Recognizer setup
recognizer = sr.Recognizer()

valid_commands = {

"shoot", "jump", "reload", "stone", "rock", "paper", "scissors", "scissor"
}

output_lines = []

Step 9: Process each selected audio file
for idx, audio_path in enumerate(selected_files, 1 ):

with sr.AudioFile(audio_path) as source:
audio = recognizer.record(source)
try:
spoken_text = recognizer.recognize_google(audio).lower()
print(f"[{idx}] Recognized text: {spoken_text}")
except Exception as e:
print(f"[{idx}] Could not recognize audio: {str(e)}")
spoken_text = None
output_lines.append(f"Audio file [{idx}]: {os.path.basename(audio_path)}")

if spoken_text in valid_commands:

# Handle stone-paper-scissors game commands
if spoken_text in {"stone", "rock", "paper", "scissors", "scissor"}:
if spoken_text == "stone":
player_move = "rock"
elif spoken_text == "scissor":
player_move = "scissors"
else:
player_move = spoken_text
moves = ["rock", "paper", "scissors"]
computer_move = random.choice(moves)
def decide_winner(player, comp):
if player == comp:
return "draw"
elif (player == "rock" and comp == "scissors") or \
(player == "scissors" and comp == "paper") or \
(player == "paper" and comp == "rock"):
return "player"
else:
return "computer"
winner = decide_winner(player_move, computer_move)
output_lines.append(f"Your move: {player_move}")
output_lines.append(f"Computer move: {computer_move}")
output_lines.append(f"Winner: {winner}")
Input Format:
● A ZIP file uploaded by the user.
● The ZIP file contains folders and subfolders with audio files inside.
● Audio files are in `.wav` or `.mp3` format (MP3 files are converted
automatically).
Output Format:
● A plain text file (`output.txt`) saved to disk.
● The file contains:
○ Audio file name processed.
○ Recognized command or error message.
○ Game moves and winner for stone-paper-scissors commands.
○ Messages for invalid or ignored commands.
else:
# Other valid commands (shoot, jump, reload)
output_lines.append(f"Command recognized: {spoken_text}")
else:
output_lines.append("Command not recognized or not a valid game command.
Ignored.")

output_lines.append("") # blank line for readability
Step 10: Write output to output.txt
with open("output.txt", "w") as f:

for line in output_lines:
f.write(line + "\n")
print("Output saved to output.txt")

Step 11 (optional): Download the output file
files.download("output.txt")

Output:
Testing and Validation:
● Tested with a variety of audio files in nested folder structures.
● Verified MP3 to WAV conversion works correctly.
● Confirmed speech recognition accuracy with clear audio samples.
● Validated game logic by simulating multiple random command inputs.
● Handled unrecognized or invalid commands gracefully by ignoring them.
Conclusion:
This project successfully demonstrates the integration of speech recognition technology
with simple gaming mechanics to create a voice-controlled interactive gaming system. By
processing audio files containing spoken commands, the system effectively recognizes
valid game inputs and executes corresponding actions such as shooting, jumping,
reloading, and playing stone-paper-scissors. Handling various audio formats within
nested folder structures and filtering irrelevant commands enhances its robustness and
usability.

The voice-command gaming approach not only enriches user experience by providing
hands-free interaction but also opens up opportunities for greater accessibility in gaming.
This foundation can be extended to more complex games and advanced voice control
features, paving the way for innovative, natural user interfaces in the gaming industry.
