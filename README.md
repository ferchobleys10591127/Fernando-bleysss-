import streamlit as st
import pyttsx3
import os

st.set_page_config(page_title="Vid SSPik - Texto a Voz")

st.title("Vid SSPik")
st.subheader("Convierte tu texto en audio")

texto = st.text_area("Escribe algo:", height=150)

if st.button("Convertir a Voz"):
    if texto.strip() != "":
        engine = pyttsx3.init()
        engine.setProperty('rate', 150)
        engine.setProperty('volume', 1.0)

        engine.save_to_file(texto, "voz.mp3")
        engine.runAndWait()

        audio_file = open("voz.mp3", "rb")
        audio_bytes = audio_file.read()
        st.audio(audio_bytes, format="audio/mp3")

        st.success("¡Texto convertido!")
    else:
        st.warning("Por favor, escribe algo.")
