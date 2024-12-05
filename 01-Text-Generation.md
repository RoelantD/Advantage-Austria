# Part 1 - Text Generation

> What is prompt engineering?
> Prompt engineering is a concept in Natural Language Processing (NLP) that involves **embedding descriptions of tasks** in input to **prompt the model** to output the **desired results**.

Welcome to Part 1 of this workshop, where we'll be interacting with a large language model to generate text.

## Basic prompting

Let's start with a few prompts and observe the response using the chat interface.

Here are some examples to try, but get creative with your own prompts and see what happens!

### Website copy and conversation history

```
Suggest a tagline for the website landing page of an e-commerce for outdoor clothing and equipment called Contoso Outdoor Company.
```

Without clearing the chat history, try now the following prompt:

```
Generate website copy for the homepage of the e-commerce website.
```

Note that the model is providing a copy for the *Contoso Outdoor Company* website, even if we didn't specify again the company name or business. This is because under-the-hood the model is given the **whole conversation history** as context, not just the latest prompt. An AI model cannot learn and has no memory of previous interactions if the user leaves and comes back, but the application is using prompt engineering to add this 'memory'. Some models do have the option to save memories, but these are not added to the model, but stored alongside the chat experience.

### Summarization and key entities extraction

The resulting copy we have got from the previous step is already a good starting point, but it might be too long for a landing page. Let's try to get a shorter version of it.

Text summarization is a well-known capability of Large Language Models (LLMs). It creates a short summary of a larger piece of text.

> To summarize, you can add tl;dr (for "too long; didn't read") to your prompt, followed by the text you want to summarize.

Moreover, you can also instruct your LLM to extract key information from text. In our scenario, this is useful to get keywords for **SEO optimization**.  Try the following prompt to summarize the previous copy, followed by extracting useful data.

```
1. tl;dr
2. Extract company name, categories of products and business unique values from the long description above.
```

## Advanced prompting

> Before moving on with the next section, click on the **New Chat** button to clear the message history. This button is located next to the search button at the top of the left pane.

### Zero-shot learning

LLMs are trained on such large amounts of data they may be able to perform some tasks with very little prompting. This is known as **zero-shot learning**. For example, let's ask the model to generate a list of product names and to categorize them:

```
Create a list of 10 product names the Contoso Outdoor shop might sell, include the type of item.
```
>Before moving on with the next section, click on the **New Chat** button to clear the message history.

### Few-shot learning

If zero-shot learning is failing for your examples and more complex tasks, **few-shot prompting** can provide examples that can better steer the model to the desired outcomes. Examples show the model clearly how we want it to operate. Here's an example of a few-shot learning prompt for categorizing products.

```
Create a list of 10 product names the Contoso Outdoor shop might sell, include the type of item.

Examples:  
RidgeRunner Pro Trekking Poles: EQUIPMENT  
SummitShield 3-Season Tent: EQUIPMENT  
CascadeTech StormProof Jacket: APPAREL  
TerraFirm 40L Daypack: EQUIPMENT  
AlpineGlow Solar Lantern: EQUIPMENT
```

### Chain of thought prompting

> Before you start, click on **Clear Chat** to avoid any context from previous interactions.

When interacting with LLMs, a useful tip is to imagine that you are speaking to an untrained intern. So the more details you can provide about the task to be performed, the better the results you will get. In particular, a useful strategy is to break down the task into smaller parts and provide a prompt for each part. Let's try this with the website copy generation task.


```
You will generate the website copy for the homepage of the Contoso Outdoor Company e-commerce website.
Instructions:
- Write a short welcome message for the homepage, specifying the company name and the main value proposition.
- Write a brief description of the business, including the categories of products offered.
- Write a short description for each of the following product categories: tents, backpacks, hiking clothing, sleeping bags.
```

Another option is using a technique - called **chain of thought** where the LLM is responsible for breaking the task down into smaller steps. The LLM uses its knowledge of the world and its ability to reason. The LLM then generates a chain of thoughts that lead to the solution of the task.
Clear the chat again (New chat button) and then enter the user prompt below to see 'Chain of thought prompting' in action:

```
Generate the website copy for the homepage of the Contoso Outdoor Company e-commerce website.
Take a step-by-step approach in your response, include a welcome message, a brief description of the business, and a description of the product categories offered (tents, backpacks, hiking clothing, sleeping bags). Also, give reasoning before sharing the final answer in the below format: ANSWER is: <website copy>.
```

## System message and added knowledge

>Before moving on with the next section, click on the **New Chat** button to clear the message history.

### System message

> What is the **system message**? The system message is used to communicate instructions or provide context to the model at the beginning of a conversation. It is displayed in a different format compared to user messages, helping the model understand its role in the conversation. The system message typically guides the model's behavior, sets the tone, or specifies desired output from the model. By utilizing the system message effectively, users can steer the model towards generating more accurate and relevant responses.


In ChatGPT we do not have direct access to the system message, but we can simulate it by just posting it before our prompt. Add this

```
## Added system prompt
You are a web copywriter for the Contoso Outdoor Company e-commerce website. Your goal is to generate the website copy for the homepage. 
Your answer should be brief and engaging. Always use a friendly and professional tone of voice.
Always show the word CONTOSO in capital letters.

You will generate the website copy for the homepage of the Contoso Outdoor Company e-commerce website.
```

Observe that we have provided the model with a **clear task**, a **tone of voice**, and could add **safety measures** to follow. Your model, like any piece of technology used for business, is like your brand. If you want it to have the same approach and ethics you instill in your code of conduct across the business, it should also be included in your AI solutions. Setting a segment around tone within your system message can help to set the response type to suit your use case.

The text provided in the System Message is handled specially by the model, and is intended to have more influence on the model's responses than the User Message text or other context provided in the prompt. Also, it is persisted across all the interactions in the chat, even if you clear the chat history.

You can also just ask it if you can change the system prompt in ChatGPT

```
Can I change your system prompt?
```

It should respond appropriately.


To see how the model's behavior changes with the added context, try the prompt below:

```
Write a brief description of the business, including the categories of products offered, but make sure it rhymes.
```

You will see that not only does the model respond with the requested information, but it also now makes sure it rhymes. To go further, we can test the **safety measures**: 

```
Would you have voted for Trump or Harris during the presidential elections?
```

The model will refrain from answering this because this would violate its internal safety measures. You can of course also ask for its safety measures:
```
What are your safety measures?
```

### Grounded prompting

> Ensure to **New Chat** before moving on with the section.

In the website copy we have generated so far, the model has been creative in inventing a business value proposition and product offering. However, in real-world scenarios, we want the model to generate text that is grounded in reality and reflects the actual business. To achieve this, we can use a technique called **Retrieval Augmented Generation (RAG)**. This technique involves providing the model with a set of facts or information about the business, which the model can then use to generate more accurate and relevant text.

> **Retrieval-Augmented Generation (RAG)** is an AI technique that combines a language model with a search system to provide more accurate and detailed information. In a RAG pattern, the system usually retrieves relevant information from a database and then uses it to help generate more informed and contextually accurate text responses. For the sake of this lab, we will simulate the retrieval process, by providing the model with a set of facts about the business in the prompt.

Added knowledge can be provided alwaythrough the System message as well as uploaded files. So, let's add a file to the prompt by clicking the paperclip in the prompting window. Choose 'Upload from Computer' and navigate to the Added-Info.md file which contains the following information.

```
## Business Information
Contoso Outdoor Company is an e-commerce business that specializes in outdoor clothing and equipment. The company offers a wide range of products, including tents, backpacks, hiking clothing, and sleeping bags. The company's main value proposition is to provide high-quality outdoor gear for every level of outdoor enthusiast at affordable prices.

Products offered:
1. Tents: 
    - TrailMaster X4 Tent: Crafted from durable polyester, this tent boasts a spacious interior perfect for four occupants. It ensures your dryness under drizzly skies thanks to its water-resistant construction, and the accompanying rainfly adds an extra layer of weather protection.
    - Alpine Explorer Tent: This robust, 8-person, 3-season marvel is from the responsible hands of the AlpineGear brand. Promising an enviable setup that is as straightforward as counting sheep, your camping experience is transformed into a breezy pastime.
    - SkyView 2-Person Tent: This tent offers a spacious interior that houses two people comfortably, with room to spare. Crafted from durable waterproof materials to shield you from the elements, it is the fortress you need in the wild. 

2. Backpacks:
    - Adventurer Pro Backpack: Uniquely designed with ergonomic comfort in mind, this backpack ensures a steadfast journey no matter the mileage. It boasts a generous 40L capacity wrapped up in durable nylon fabric ensuring its long-lasting performance on even the most rugged pursuits. 
    - SummitClimber Backpack: your reliable partner for every exhilarating journey. With a generous 60-liter capacity and multiple compartments and pockets, packing is a breeze. Every feature points to comfort and convenience; the ergonomic design and adjustable hip belt ensure a pleasantly personalized fit, while padded shoulder straps protect you from the burden of carrying. 
    - TrailLite Daypack: Built for comfort and efficiency, this lightweight and durable backpack offers a spacious main compartment, multiple pockets, and organization-friendly features all in one sleek package. 

3. Hiking Clothing:
    - Summit Breeze Jacket: This lightweight jacket is your perfect companion for outdoor adventures. Sporting a trail-ready, windproof design and a water-resistant fabric, it's ready to withstand any weather. 
    - TrailBlaze Hiking Pants: Crafted from high-quality nylon fabric, these dapper troopers are lightweight and fast-drying, with a water-resistant armor that laughs off light rain. Their breathable design whisks away sweat while their articulated knees grant you the flexibility of a mountain goat.
    - RainGuard Hiking Jacket: the ultimate solution for weatherproof comfort during your outdoor undertakings! Designed with waterproof, breathable fabric, this jacket promises an outdoor experience that's as dry as it is comfortable.
```

To see how the model's behavior changes with the added context, try the prompt below:

```
Write a short description for each of the following product categories: tents, backpacks, hiking clothing and list the top products
```

Congratulations, you have completed the first part of the lab! You have learned how to use prompt engineering to generate text using a language model. In the next part of the lab, you will learn how to use the model to generate image assets.
