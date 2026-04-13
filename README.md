<img width="1440" height="3014" alt="image" src="https://github.com/user-attachments/assets/f86d5ebf-8e15-4e95-b031-00b902cef488" />

**Source code**

import streamlit as st
from langchain_ollama import ChatOllama
from langchain_core.messages import HumanMessage, SystemMessage, AIMessage

st.title("Chatbot")

# initialize chat history
if "messages" not in st.session_state:
    st.session_state.messages = []
    st.session_state.messages.append(SystemMessage("Act like an teacher"))

# display chat messages from history on app rerun
for message in st.session_state.messages:
    if isinstance(message, HumanMessage):
        with st.chat_message("user"):
            st.markdown(message.content)
    elif isinstance(message, AIMessage):
        with st.chat_message("assistant"):
            st.markdown(message.content)

# create the bar where we can type messages
prompt = st.chat_input("How can i help you today?")

# did the user submit a prompt?
if prompt:
    with st.chat_message("user"):
        st.markdown(prompt)
    st.session_state.messages.append(HumanMessage(prompt))

    llm = ChatOllama(
        model="llama3",
        temperature=2
    )
    result = llm.invoke(st.session_state.messages).content

    with st.chat_message("assistant"):
        st.markdown(result)
        st.session_state.messages.append(AIMessage(result))
    



**Output**

<img width="1238" height="814" alt="image" src="https://github.com/user-attachments/assets/641bd647-6c71-4918-8224-892ef5d17517" />

<img width="1283" height="840" alt="image" src="https://github.com/user-attachments/assets/707bb8f4-9bea-439e-b39d-b152484c5d0b" />
