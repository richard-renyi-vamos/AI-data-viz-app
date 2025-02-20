CHATGPT CONVERSATION

****************

create an AI data visualization app with PYTHON and CHATGPT
ChatGPT said:
Here's a basic AI-powered data visualization app using Python and ChatGPT. It allows users to upload a dataset (CSV file), analyze it, and generate visualizations using Matplotlib and Seaborn. The app will be interactive and let users ask questions about the dataset.

Ai Data Viz App

Answer in chat instead
Your AI-powered data visualization app is set up! 🚀 It allows users to upload a CSV file, generate scatter plots, and ask AI-driven questions about the dataset. Let me know if you need any enhancements! 😊📊


*****************

import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import openai

# Streamlit App Title
st.title("AI-Powered Data Visualization App")

# Upload CSV File
uploaded_file = st.file_uploader("Upload your CSV file", type=["csv"])

if uploaded_file is not None:
    df = pd.read_csv(uploaded_file)
    st.write("### Preview of Dataset:")
    st.write(df.head())
    
    # Basic Stats
    st.write("### Dataset Summary:")
    st.write(df.describe())
    
    # Select Columns for Visualization
    st.write("### Generate Visualizations")
    col_x = st.selectbox("Select X-axis", df.columns)
    col_y = st.selectbox("Select Y-axis", df.columns)
    
    # Plot
    fig, ax = plt.subplots()
    sns.scatterplot(data=df, x=col_x, y=col_y, ax=ax)
    st.pyplot(fig)
    
    # AI-Powered Insights
    st.write("### Ask AI About Your Data")
    question = st.text_input("Enter your question about the dataset")
    
    if st.button("Get AI Insights"):
        openai.api_key = "your-openai-api-key"  # Replace with your API Key
        prompt = f"Analyze the following dataset and answer: {question}. Dataset:
        {df.head().to_string()}"
        
        response = openai.ChatCompletion.create(
            model="gpt-4",
            messages=[{"role": "system", "content": "You are an AI data analyst."},
                      {"role": "user", "content": prompt}]
        )
        
        st.write("**AI Response:**", response["choices"][0]["message"]["content"])
