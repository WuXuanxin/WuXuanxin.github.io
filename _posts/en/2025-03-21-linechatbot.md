---
layout: post
title: How to Build a LINE ChatGPT Chatbot with Zero Coding Effort
date: 2025-03-20 17:00:00
description: 
tags: ZeroCodingChatbot
categories: Workflow 
---

In this blog, I’ll share my experience of creating a LINE chatbot powered by OpenAI’s ChatGPT. The goal is to attach a LINE official account with an auto-reply chatbot function that responds based on the user’s current message and conversation history. The best part? No coding is required!

<div class="container" style="display: flex; gap: 20px;">
  <!-- Left Column: Image and Description -->
  <section class="left-column" style="flex: 1;">
    <header>
      <h2>Example: Chatbot Conversation</h2>
    </header>
    <article>
      <p>Here is an example of a conversation between a user and a chatbot, showcasing the chatbot's context-aware responses:</p>
      {% include figure.liquid 
         loading="eager" 
         path="assets/img/zero_code_chatbot/example.jpg"
         class="img-fluid rounded z-depth-1" 
         data-zoomable="true" 
         alt="Example of a chatbot conversation"
         width="60%"
         height="40%"
      %}
      <p>To achieve this, you will need the following tools:</p>
      <ol>
        <li><strong>OpenAI API</strong></li>
        <li><strong>LINE Official Account</strong></li>
        <li><strong>MAKE Account</strong>: To automate the workflow between LINE and OpenAI.</li>
      </ol>
      <p>If you haven't set them up yet, refer to the instructions on the right. Skip this section if you already have them.</p>
    </article>
  </section>

  <!-- Right Column: Setup Instructions -->
  <aside class="right-column" style="flex: 1;">
    <header>
      <h1>Setup Instructions</h1>
    </header>
    <article>
      <p>If you haven't set up the required tools yet, follow the steps below. Skip this section if you already have them.</p>

      <section>
        <h2>1. Create an OpenAI Account and Get Your API Key</h2>
        <h3>If you don’t have an OpenAI account:</h3>
        <ol>
          <li>Sign up at <a href="https://auth.openai.com/create-account" target="_blank">OpenAI Create Account</a>.</li>
          <li>Generate your first API key during account creation or later.
            <strong>Important</strong>: Save your API key locally. You won’t be able to see it again!</li>
          <li>Check OpenAI’s <a href="https://openai.com/pricing" target="_blank">pricing</a> and decide how many credits to purchase.</li>
        </ol>
        <h3>If you already have an account:</h3>
        <ol>
          <li>Log in at <a href="https://auth.openai.com/log-in" target="_blank">OpenAI Log In</a>.</li>
          <li>Go to <strong>Settings ⚙️ → PROJECT → API keys → + Create new secret key</strong>.</li>
        </ol>
      </section>

      <section>
        <h2>2. Create a LINE Official Account</h2>
        <p>Follow the official instructions to create a LINE Official Account:</p>
        <p><a href="https://help2.line.me/official_account/android/categoryId/20010172/pc?lang=en&contentId=20013134" target="_blank">LINE Official Account Setup Guide</a></p>
      </section>

      <section>
        <h2>3. Get Your Channel Access Token and Connect to MAKE</h2>
        <ol>
          <li>Create a <strong>MAKE</strong> account (formerly Integromat).</li>
          <li>Connect it to LINE Developers. Refer to this guide (in Japanese) for detailed steps:
            <a href="https://kiko-an.com/make-integromatlinebot/" target="_blank">MAKE and LINE Integration Guide</a>.</li>
        </ol>
      </section>

      <footer>
        <p><strong>Note</strong>: Ensure you have all the required credentials (API keys, tokens, etc.) saved securely before proceeding.</p>
      </footer>
    </article>
  </aside>
</div>
   ---

   ## Step 2: Set Up LINE

   ### Create a LINE Official Account
   1. Follow the official instructions to create a LINE official account:  
      [https://help2.line.me/official_account/android/categoryId/20010172/pc?lang=en&contentId=20013134](https://help2.line.me/official_account/android/categoryId/20010172/pc?lang=en&contentId=20013134).

   ### Get Your Channel Access Token
      Create a **MAKE** account and connect it to LINE Developers.
      Refer to this guide (in Japanese) for detailed steps:  
      [https://kiko-an.com/make-integromatlinebot/](https://kiko-an.com/make-integromatlinebot/).


  </div>
</div>


---

## Step 3: Build the Chatbot Workflow in MAKE

I created a chatbot for Japanese language learning. Here’s how it works:

### Overview
- The chatbot receives a user’s message, retrieves conversation history from the database, aggregates the data, sends it to OpenAI, and replies to the user.

### Behind the Scenes: MAKE Scenarios

1. **LINE → Watch Events**: Add your webhook to listen for user messages.
2. **Data Store Search Records**:
   - Search the user’s message history within the last 2 minutes (adjust the `{-2}` value as needed).
3. **Text Aggregator**:
   - Aggregate the current query and historical queries from the Data Store.
4. **Data Store**:
   - Search the chatbot’s reply history to the user within the last 2 minutes.
5. **Tools**:
   - Aggregate the conversation history and current query to prepare the input for OpenAI.
6. **OpenAI**:
   - Configure the model (e.g., GPT-3.5 or GPT-4).
   - Set up messages:
     - **Message 1**: Your custom prompt (edit in Text Content).
     - **Message 2**: User query history (from the first Data Store).
     - **Message 3**: Chatbot reply history (from the second Data Store).
     - **Message 4**: Current user query.
   - Adjust hyperparameters like `temperature` and `top_p` as needed.
7. **Ignore Module**:
   - Acts as an error handler to keep the scenario running even if errors occur. Learn more [here](https://www.make.com/en/help/errors/error-handlers/ignore-error-handler).
8. **LINE → Send a Reply Message**:
   - Send the chatbot’s reply (from OpenAI) back to the user.
9. **Ignore Module**:
   - Again, acts as an error handler to keep the scenario running even if errors occur. 
10. **Data Store**:
   - Append the user’s query to the Data Store.
11. **Data Store**:
    - Append the chatbot’s reply to the Data Store.

---

## Final Thoughts
Building a LINE chatbot with OpenAI and Make is a powerful way to create intelligent, automated interactions. Whether you’re building a language-learning bot or a customer support assistant, this no-code approach makes it accessible to everyone.

Feel free to tweak the workflow to suit your needs, and let me know if you have any questions!

---

**Happy bot-building!** 🚀