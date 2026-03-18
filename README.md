# ai-content-generator

import streamlit as st
from openai import OpenAI

client = OpenAI(api_key="YOUR_API_KEY")

st.title("AI Content Generator")

content_type = st.selectbox(
    "Select Content Type",
    ["Instagram Caption", "YouTube Script", "Blog Post"]
)

tone = st.selectbox(
    "Select Tone",
    ["Professional", "Funny", "Motivational"]
)

topic = st.text_input("Enter Topic")

def generate_prompt(content_type, tone, topic):
    return f"""
    Create a {tone} {content_type} about {topic}.
    Include engaging and high-quality content.
    """

if st.button("Generate Content"):
    if topic:
        prompt = generate_prompt(content_type, tone, topic)

        response = client.chat.completions.create(
            model="gpt-4o-mini",
            messages=[{"role": "user", "content": prompt}]
        )

        st.write("### Generated Content:")
        st.write(response.choices[0].message.content)
