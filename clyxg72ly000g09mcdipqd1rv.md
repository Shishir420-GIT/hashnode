---
title: "Image Menu to HTML Menu"
seoTitle: "Image Menu to HTML Menu"
seoDescription: "A generative AI application to convert your Image of a menu card to an HTML webpage in seconds, using Claude 3 sonnet from Amazon Bedrock and Python."
datePublished: Mon Jul 22 2024 20:37:13 GMT+0000 (Coordinated Universal Time)
cuid: clyxg72ly000g09mcdipqd1rv
slug: image-menu-to-html-menu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1750700922127/b2698f15-d18b-4ccd-9b8f-fdacba50730a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1750700891411/72585d7e-9b79-4bc2-848b-91e8b05fb6e5.png
tags: aws, bedrock, genai, aifortomorrow

---

## Introduction:

With advancing technology, we are seeing how some cafes and restaurants are offering their customers online menus for ordering instead of traditional physical menu cards.

But for smaller businesses to do this, they would need to either hire someone or learn basic HTML to create a simple webpage. Then, they would have to sit to add each item and its price one by one manually, and later figure out hosting and its cost.

Well, we thought of addressing the first hurdle with the help of AI. Imagine if AI could extract all the items with their prices, format them properly, and give you an HTML file with CSS included. You don't need to imagine anymore because today I will show you exactly how to do that and how YOU can create your first GenAI with us today.

## Prerequisites:

* Python 3.10+
    
* Required packages: Streamlit, Pillow (PIL), Boto3, base64
    
* An IDE for writing code (If you need it)
    
* Git for cloning the code to your local machine.
    
* Claude 3 Sonnet model access Amazon Bedrock
    
* Access Credentials to Amazon Bedrock
    

*Note: We are using the Amazon bedrock platform for accessing Claude's sonnet model for this tutorial; however, you can choose an AI model of your choice, like Gemini Pro from Google Cloud, and the principle will remain the same.*

*<mark>Note: This tutorial is going to incur some costs, hence please be cautious.</mark>*

## Key Features:

* Image upload functionality
    
* AI-powered image analysis and data extraction.
    
* AI-powered HTML generation
    
* Option to regenerate HTML and preview it
    

## Break down the task into Steps:

### Step 1: Make sure you have access to an AI model in Amazon Bedrock.

* Navigate to the Amazon Bedrock service in your AWS console &gt;&gt; Scroll down on the left panel till you see 'Model Access' &gt;&gt; Click on 'Model Access'.
    
* Here you can see a list of models available in Bedrock and the ones you have access to.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721674847640/fcef149b-dfef-49fe-a344-755874500176.png align="center")
    
* Note that access is not provided by default. if you don't have access, select Modify access at the top of the page and Request access.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721674961364/b38b5d0a-a221-43b1-af76-b22d7e00991a.png align="center")
    
* Once your access is approved, you are good to go ahead with the next steps.
    

### Step 2: Create Access keys for your user to access the Bedrock via your Python code.

* Navigate to IAM users in your AWS Console &gt;&gt; Select the user you want to generate access Keys for.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721675759946/e60f7014-b0fb-4c58-93df-0aecda7955fd.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721675908132/0ada4310-f26b-44f7-b7d9-5f8a09bd7584.png align="center")
    
* Select the Local code as shown in the image below.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721675960084/553a58d5-dd9e-48c3-8549-68425d5d6818.png align="center")
    
* Copy the Access Key and Secret Access Key, store them, you'll need them in the next steps.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721676233586/2028db81-c590-4c9c-b22a-d674684f29fb.png align="center")
    
* ***Now that we are done with our LLM access, we move on to the next part which is, actually implementing it.***
    

### Step 3: Setting up your coding environment.

1. Open your terminal, clone the repository and navigate to the Image-To-Menu directory.
    

```plaintext
git clone https://github.com/Shishir420-GIT/GenAI-Usecases.git
cd Image-To-Menu
```

2. Install the required packages
    

```plaintext
pip install streamlit pillow boto3 base64
```

3. Set up AWS credentials:
    

* Create a `.streamlit/secrets.toml` file in the project directory.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721677313853/b39597af-0898-4cad-ac0d-a49d07f73aa8.png align="center")
    
* Add your AWS credentials:
    
    ```plaintext
    AWS_ACCESS_KEY_ID = "your_access_key_id"
    AWS_SECRET_ACCESS_KEY = "your_secret_access_key"
    ```
    
* Make sure you add this file in the .gitignore file.
    

***If you have reached this step, then give yourself a pat on the back, you are now ready to run your code.***

### Step 4: Running the code.

1. Make sure you are in the same folder as the main code file and run the below command,
    
    ```plaintext
    streamlit run image_to_menu_html.py
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721679068836/f4f02731-33ca-4a78-82d5-45e4ce6a5b5f.png align="center")
    
2. Open the provided URL in your web browser, your UI for the application should be as below:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721677533389/4ab19d56-f66f-45cd-abcd-934c8b7a881b.png align="center")
    
    *For creating the UI, we are using a Python library called Streamlit.*
    
3. Click on Browse Image and select an Image Menu to be converted to an HTML Menu. Once the Image is selected, you'll see the 'Extract Menu Content' button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721677963087/9673017f-d3f2-4d6b-af2f-8dbea734b557.png align="center")
    
4. Click on the "Extract Menu Content" to analyse and extract the contents of the image.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678042669/74a057fe-2186-43e7-8f8e-293af472cefe.png align="center")
    
5. Observe the Extracted output, at the bottom, you can now see a 'Generate HTML'. button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678211028/c67582b0-909c-41c7-b138-f34b0b8f2f1b.png align="center")
    
6. Now, click the generate HTML button
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678310239/be92e665-cdc4-457e-8f16-e0df0c744853.png align="center")
    
7. Once the HTML is generated, you'll see the download HTML and Preview your HTML buttons.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678601247/1e10a543-dde0-451d-8ca2-89116a37e8b0.png align="center")
    
8. And just like that, your HTML is created, you can preview and regenerate it if you want, or download it to use as a webpage using the 'Preview' and 'Download HTML file' buttons, respectively.
    
9. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678716550/91dadf06-5828-4b8e-93a2-7676b3dec535.png align="center")
    
    Output of Preview HTML.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678790395/008bd1b7-2174-408b-9606-d1efeadc24a1.png align="center")
    
10. You can download and open the webpage to review as well.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721678942530/c5f16280-505f-48db-8e34-efc1d61c9921.png align="center")
    
    ### Step 5: Deployment.
    
    * We are not covering deployment as of now for this project. However, Streamlit provides community hosting, so you can probably check that out.
        
    * For Streamlit Cloud deployment, add your AWS credentials in the Streamlit Cloud dashboard under the "Secrets" section.
        
    * For other deployment options, ensure to set the AWS credentials as environment variables securely.
        

## Closure:

* You have now successfully used AWS Bedrock and the Claude 3 Sonnet AI model for an image to create an HTML page creation application.
    
* This application uses AWS Bedrock, which may incur costs. Please review AWS pricing before extended use.
    
* Ensure your AWS credentials have the necessary permissions to access Bedrock services.
    

---

---

Thanks for coming this far in the article. I hope I was able to explain the concept well enough. If you face any issues, please feel free to reach out to me; I'd be happy to help.

## 🔗 Let’s stay connected!

[**🌐 Linktree**](https://linktr.ee/shishirsrivastav)| [**🐦 X**](https://x.com/shishir_who)| [**📸 Instagram**](https://www.instagram.com/programmatic.ly)| [**▶️ YouTube**](https://www.youtube.com/channel/UCCZiCzPtg9pmDwChJ4ROIpA) [**✍️ Hashnode**](https://hashnode.com/@ShishirSrivastav)| [**💻 GitHub**](https://github.com/Shishir420-GIT)| [**🔗 LinkedIn**](https://www.linkedin.com/in/shishir-srivastav)| [**🤝 Topmate**](https://topmate.io/shishir_srivastav) [**🏅 Credly**](https://www.credly.com/users/shishir-srivastav-who)

© 2024 Shishir Srivastav. All rights reserved.