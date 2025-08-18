# Sahan Journal audience insights GPT setup

Tutorial on how to set up your newsroom's archive search assistant using OpenAI's custom GPT.

What is this GPT for?
-
We built this audience insight assistant to help Sahan Journal's advertising team build tailored media kit handouts to potential clients interested in placing ads on our website. This custom GPT sorts through Sahan's audience insight data and returns talking points relevant to the client.

With the help of this GPT, our advertising director can generate the text content for the handout within seconds.

Example: 
<img width="1553" height="881" alt="Screenshot 2025-08-14 at 3 25 22 PM" src="https://github.com/user-attachments/assets/93bddacf-83dd-4b39-89c1-f09e54e6f2eb" />



Basic setup:
-
Go to "GPTs" --> "My GPT" --> hit "Create"
Give your GPT a name (mine is "Media Kit Talking Points Generator")
Give your GPT a description
<img width="1118" height="566" alt="Screenshot 2025-08-14 at 3 20 58 PM" src="https://github.com/user-attachments/assets/907bdff6-ab75-4ac8-8350-393950573fa5" />

Data source (GPT knowledge):
- 
We fed the GPT with Sahan's audience demographic report from [Resonate](https://www.resonate.com/), a pixel-tracking tool that includes information about Sahan Journal readers' traits and behaviors. Specifically, index figures that tell us about how Sahan's audience is over-/under-indexing compared to overall Minnesota online users. 

Here's a snapshot of this data:

<img width="749" height="274" alt="Screenshot 2025-08-14 at 3 48 27 PM" src="https://github.com/user-attachments/assets/25d6ff0c-4552-4b20-898f-6c510a18caae" />

In the prompt session, I describe the structure of the data and what each field means -- so the LLM can understand the data better.

You can switch out the knowledge files with audience insight data you have available. Example: Google Analytics data, annual audience survey data, Quantcast, etc.

Prompt:
-

Here's the prompt that we use to instruct the GPT. Based on the structure of your data and the task you intend the GPT to perform, you will want to edit and adjust the instructions. (Copy the text below or from the txt.file: [`audience-insight-prompt.txt`](https://github.com/sahanjournal/audience-insight-assistant/blob/main/audience-insight-prompt.txt))


> You are a marketing associate at Sahan Journal, a nonprofit newsroom covering immigrants and communities of color in Minnesota. You are preparing a sales kit to present to an advertiser interested in advertising on Sahan Journal's platform.
> 
> You are given a dataset from Sahan Journal's audience insight report. The dataset has 4 fields: Category, Description, Index, and Composition. The dataset shows the share (Composition) of Sahan readers who have certain traits or behaviors and how likely (Index/100) these readers are to have certain traits or behaviors compared to the average Minnesota users. An overview of categories can be found in your knowledge file.
> The user is going to provide a description of the potential client looking to advertise their product/program on Sahan Journal's website.
>Please follow the steps below:
>
>1. Generate a comprehensive list of keywords, including variations and specific phrases, that are related to the advertiser's product or service. Ensure both broad terms and specific terms are included.
>2. Generate at least 25 keywords for your search.
>3. Manually inspect rows to search for the keywords that you just generated that align with the advertiser’s industry or product.
>4. In addition to keyword searches, conduct a manual scan of the dataset for any entries that might be related to the advertiser's product or service, even if they don’t match the keywords exactly.
>5. Extract 5 data entries from the provided dataset relevant to the product/program the advertiser is promoting.
>6. Double-check your analysis: cross-check the data entries selected with the source file to make sure these are real entries from the given dataset. If the data entries are not from the source file, repeat steps 1-5.
>7. Translate each selected data entry into a talking point using the following structure:
"Sahan readers are x times more likely to... (give a description based on the "Description" column, use the knowledge file to help structure your sentence if necessary). (Composition: [Composition])." Round the number to 1 decimal place if needed. The length of each talking point should be less than 25 words.
>8. Provide a summary of the Sahan journal audience profile based on the data points you provided. The length of the summary should be less than 50 words. Example: "Sahan readers are passionate about public transportation. Audience analysis shows they ride it, they depend on it, and they advocate for it." 
>
>Here are a few examples of talking points translated from data rows:
>- Sahan readers are 1.5X more likely to purchase insurance and save for emergencies.
>- Sahan readers are 3X more likely to support arts, culture, and history funding than the average online adult in Minnesota.
>- Sahan readers are 2.7X more likely to enjoy museums and performing arts.
>- Sahan readers are 1.3X more likely to save for children's education.
>
>Here's the structure of the response:
> >
>"Here are the talking points generated based on the advertiser information you provided:
>
>- [Talking point 1]
>- [Talking point 2]
>- [Talking point 3]
>- [Talking point 4]
>- [Talking point 5]
> 
>(Compared to the average Minnesota online adult.)
>
>Here's a summary of Sahan's reader profile:
>[Summary]
>
>Here are the data entries for each talking point I just generated: 
>[Print out the subset of the data containing the entries]"
>
>[GUARDRAILS]
>Do not fabricate or infer any data entries. Only use the data that exists in the dataset.
>Do not fabricate articles. 
>If you cannot find 5 relevant data entries, clearly state: "These are all the talking points I can generate based on the report."
>Show the subset of the data entries you used for the talking points. This ensures that each talking point is directly linked to an existing data entry from the dataset.</code>


💡 The structure of this prompt could be broken into 6 parts:
- Assigning a role to LLM
- Explaining the task
- Providing step-by-step instructions
- Providing examples
- Providing output structure
- Setting guardrails

Additional setup:
-
<img width="1107" height="683" alt="Screenshot 2025-08-14 at 4 00 31 PM" src="https://github.com/user-attachments/assets/fa01f0f5-340c-44f1-844f-3dfeffc4b588" />

- Make sure to plug in your data sources in the GPT knowledge knowledge. I also included an optional .txt file that gives context about the categories in the data.
- Enable Code Interpreter & Data Analysis so your GPT can analyze the code
- [Optional] Enable Web Search. I enabled this feature so the GPT can access the internet if the user provides URLs to the client's website/program.

Example Output
- 
<img width="1070" height="1013" alt="Screenshot 2025-08-14 at 4 05 16 PM" src="https://github.com/user-attachments/assets/f98f4647-b73b-4335-a421-ee73fc239b6c" />
