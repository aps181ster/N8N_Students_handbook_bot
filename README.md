**Student Handbook Telegram Bot Flow**

This project demonstrates the creation of a Student Handbook Assistant chatbot powered by Retrieval-Augmented Generation (RAG) using n8n, Telegram, OpenAI, Pinecone, and Google Drive. The bot can provide answers based solely on the content of an uploaded student handbook.
Prerequisites
Before importing and running the workflow, ensure you have the following setup:
1. n8n Account
•	Create an account at n8n.io.
2. API Keys & Credentials
•	Telegram API:
Create a bot using BotFather and obtain your bot token.
•	OpenAI API Key:
Sign up at OpenAI and get an API key for embeddings and chat models.
•	Pinecone API Key:
Create an account on Pinecone and get your API Key.
•	Google Drive API Credentials:
Set up OAuth2.0 credentials from Google Cloud Console, enable the Google Drive API, and download the credentials.json file.
3. Set up n8n Environment
•	Install n8n on your machine using Docker, or use their hosted service.
•	Access your n8n instance via the provided URL.
Steps to Import & Test the Flow
1. Import Workflow
•	Open your n8n instance.
•	Go to the Workflows section and click on Import.
•	Copy the JSON from the exported workflow file or use the provided JSON.
•	Paste the JSON into the import section and click Import.
Alternatively, you can upload the workflow JSON files directly (e.g., Telegram_Studnt_bot_Workflow.json and Students Vector Creation.json).
2. Configure Credentials
After importing the workflow, you need to configure the necessary credentials for the services:

Telegram
•	In the n8n credentials section, add your Telegram Bot API key.
OpenAI
•	Add your OpenAI API key for embedding generation and chatbot functionality.
Pinecone
•	Set up your Pinecone API key and the index you are using (e.g., "students-handbook").
Google Drive
•	Link your Google Drive account using OAuth2.0 credentials for document upload and access.
3. Test the Workflow
Once you have configured all the credentials, you can proceed to test the workflow:
Step 1: Upload the Student Handbook Document
•	Upload the Student Handbook.docx or any other relevant student document to your Google Drive.
•	Ensure the folder being watched by n8n (referenced in the workflow) contains the document.
•	The workflow will automatically trigger when the document is uploaded.
Step 2: Test Document Chunking & Embedding
•	The document will be chunked and embedded into Pinecone.
•	Ensure the chunks are correctly stored in Pinecone, and that the vector data is being used in subsequent queries.
Step 3: Use Telegram to Ask Questions
•	Send a query to your Telegram bot (e.g., "What is the grading system?").
•	The bot will retrieve relevant chunks from Pinecone based on your query and generate an answer using OpenAI.
•	Ensure the response is aligned with the document content (for example, if the question is about grading, it should return the relevant section from the handbook).
Step 4: Test Edge Cases
•	Ask questions that are not related to the student handbook, like “What is the weather today?”
•	The bot should reply with:
“Sorry! I can’t find relevant information from the student handbook.”

4. Test Fallback Logic
•	Test various queries to ensure the bot only returns relevant, document-based information and politely refuses off-topic questions.
Workflow Architecture
The workflow is composed of two major segments:
1.	Document Ingestion Flow:
o	Monitors the Google Drive folder for new uploads.
o	Extracts and processes the document into chunks.
o	Generates embeddings using OpenAI and stores them in Pinecone.
2.	Telegram Query Flow:
o	Receives user queries through Telegram.
o	Queries Pinecone for the most relevant chunks.
o	Uses OpenAI’s model to generate a response.
o	Sends the response back to the user on Telegram.
Troubleshooting
If you encounter any issues, ensure the following:
•	All credentials are correctly configured in n8n.
•	The Google Drive folder being watched by the workflow contains the document you want to use.
•	Pinecone has the appropriate index and API keys.
•	OpenAI keys are valid and the model is properly set up.
Additional Notes
•	You can modify the system prompt in the Telegram Query Flow if you need the bot to handle different document types or answer differently based on the document content.
•	If you wish to add more documents to the Pinecone index, simply upload them to the Google Drive folder, and the system will automatically process and index them.

