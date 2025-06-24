# Audio Analysis for Autism Detection Research

This Jupyter Notebook outlines a series of audio processing steps aimed at extracting features that could potentially be relevant for autism detection research. It utilizes OpenAI's Whisper model for transcription and the Librosa library for analyzing acoustic features like speech speed, pitch, and volume.

## Notebook Overview

The notebook is structured as follows:

1.  **Transcription:**
    *   **Model:** Utilizes the `tiny` model of OpenAI's Whisper for speech-to-text transcription.
    *   **Rationale for `tiny` model:**
        *   **Small Size (39M parameters):** Requires very little memory and compute power.
        *   **Low VRAM Usage (~1 GB):** Can run on older or low-end GPUs or even CPUs.
        *   **Fast Speed (~10x):** Offers quick transcription, ideal for real-time or near-real-time use, or processing large datasets efficiently.
        *   **Two Options (English-only & Multilingual):** Choice available based on language needs without increasing size.
        *   **Conclusion:** The `tiny` model balances speed and efficiency, making it suitable for devices with limited hardware resources or for applications where fast processing is prioritized over perfect accuracy.
    *   **Output:** Generates a full transcript along with segment-level details (text, start time, end time).
    *   **GitHub Link:** [OpenAI Whisper](https://github.com/openai/whisper)

2.  **Speech Speed Analysis:**
    *   **Method:** Calculates the speed of spoken words (or characters for languages like Chinese) from the Whisper transcript.
    *   **Calculation:**
        1.  The transcript is analyzed in short, consecutive time intervals (e.g., every 5 seconds with a 1-second step).
        2.  For each interval, the number of words (or characters) from segments starting within that window is counted.
        3.  This count is divided by the window duration to get a "speed" measurement (words/characters per second).
    *   **Visualization:** A plot is generated showing the speech speed variation over time.
        *   The horizontal axis represents the timeline of the recording.
        *   The vertical axis shows the calculated speech speed.
        *   This helps identify patterns in speaking rhythm and periods of faster or slower speech.

3.  **Pitch Variation Analysis:**
    *   **Library:** Uses Librosa for audio analysis.
    *   **Hardware Requirements for Librosa (Basic):**
        *   **CPU:** Modern multi-core CPU.
        *   **RAM:** At least 4 GB.
        *   **Storage:** Sufficient for audio files.
        *   **OS:** Linux, macOS, Windows.
    *   **Method:**
        1.  **Understanding Pitch:** Pitch is the perceived highness or lowness of a sound, its fundamental frequency (measured in Hertz - Hz).
        2.  **Extraction:** Librosa analyzes the audio in tiny segments, using algorithms (like `piptrack`) to estimate the most prominent pitch at each instant.
    *   **Visualization:** A plot shows how the detected pitch changes over time.
        *   The horizontal axis is time.
        *   The vertical axis is pitch (Hz).
        *   The line reveals the melody or intonation contour of the speech.

4.  **Volume Variation Analysis:**
    *   **Library:** Uses Librosa.
    *   **Method:**
        1.  **Understanding Volume:** Volume refers to the loudness or intensity of a sound, often measured by its Root Mean Square (RMS) energy.
        2.  **Extraction:** Librosa divides the audio into short frames and calculates the RMS energy for each, indicating loudness.
    *   **Visualization:** A plot illustrates how the volume (RMS energy) fluctuates.
        *   The horizontal axis is time.
        *   The vertical axis is volume (RMS energy).
        *   The line shows the "volume contour," highlighting changes in loudness.

## Setup and Usage

1.  **Environment:** This notebook is designed to run in a Python environment, preferably in Google Colab or a local Jupyter setup.
2.  **Dependencies:**
    *   Install OpenAI Whisper:
        ```bash
        !pip install -U openai-whisper
        ```
    *   Librosa and Matplotlib are also required. These are usually pre-installed in Colab or can be installed via pip:
        ```bash
        !pip install librosa matplotlib numpy
        ```
3.  **Audio File:**
    *   Replace the placeholder `audio_path` in the code cells with the actual path to your audio file (e.g., an MP3 file).
    *   Example: `audio_path = '/content/your_audio_file.mp3'`
4.  **Running the Notebook:** Execute the cells sequentially to perform transcription and then the acoustic analyses. The plots for speed, pitch, and volume variation will be displayed inline.

## Output

The notebook will output:

*   The full transcribed text from the audio file.
*   A list of dictionaries detailing the words per second (WPS) or characters per second (CPS) for each time window.
*   A line graph visualizing the "Speech Speed Variation Over Time."
*   A line graph visualizing the "Pitch Variation Over Time."
*   A line graph visualizing the "Volume Variation Over Time."

## Potential Applications in Autism Detection Research

The extracted features (transcription content, speech rate, pitch contours, volume dynamics) can serve as inputs for machine learning models aimed at identifying vocal patterns or characteristics that might be associated with Autism Spectrum Disorder (ASD). This notebook provides a foundational toolkit for such feature extraction.

## Disclaimer

This notebook and its outputs are for research and informational purposes. The acoustic features extracted are not, by themselves, diagnostic of any condition. Any application in a clinical or diagnostic context should be done with appropriate validation and by qualified professionals.
