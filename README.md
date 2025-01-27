# Audify: The Blog/Book Narrator Using Amazon S3 & Amazon Polly

Audify is a powerful text-to-speech application that utilizes **Amazon Polly** to transform written content into high-quality audio. Designed for authors, bloggers, and educators, Audify enhances accessibility and engagement by turning words into natural-sounding voices.

## Features
- **Content Accessibility**: Enables visually impaired users to listen to written information.
- **Learning Support**: Assists users in learning by providing audio versions of content.
- **Convenience**: Users can listen to blogs/books while multitasking.
- **Extended Content Reach**: Increases audience engagement by providing an additional medium for content consumption.

---

## Architecture Overview

1. **Client/User**: Uploads a `.txt` file to the **Source S3 Bucket**.
2. **Source S3 Bucket**: Stores uploaded text files and triggers the **Lambda Function**.
3. **Lambda Function**: Processes the uploaded file using **Amazon Polly** to convert text into audio.
4. **Amazon Polly**: Synthesizes realistic speech from the text using the **Standard Voice Engine**.
5. **Destination S3 Bucket**: Stores the resulting audio file for download.

---

## Prerequisites

- An AWS Account (AWS Free Tier is sufficient for basic functionality).
- Basic knowledge of AWS services like **S3**, **Lambda**, and **IAM**.
- Python 3.8 or higher for Lambda function code.

---

## Setup Guide

### Step 1: AWS Account Setup
Sign up for an AWS Free Tier account if you don’t have one already.

### Step 2: Create S3 Buckets
Create two S3 buckets:
- **Source Bucket**: e.g., `mayuresh-amc-polly-source-bucket`
- **Destination Bucket**: e.g., `mayuresh-amc-polly-destination-bucket`

### Step 3: Configure IAM Policy
1. Create an IAM policy with necessary permissions for S3 and Polly.
2. Attach the policy to an IAM role.

### Step 4: Create IAM Role
- Role Name: `mayuresh-amc-polly-lambda-role`
- Attach these policies:
  - Custom policy (`mayuresh-amc-polly-lambda-policy`)
  - `AWSLambdaBasicExecutionRole`

### Step 5: Create Lambda Function
1. Name: `TextToSpeechFunction`
2. Runtime: Python 3.8
3. Assign the role created in Step 4.
4. Add environment variables:
   - `SOURCE_BUCKET`: Your source bucket name.
   - `DESTINATION_BUCKET`: Your destination bucket name.

### Step 6: Configure S3 Event Notification
Set up an event notification in the **Source Bucket** to trigger the Lambda function when a `.txt` file is uploaded.

### Step 7: Write Lambda Code
Write and deploy the Python code for text-to-speech conversion. The Lambda function will:
- Extract text from the uploaded file.
- Use Amazon Polly to synthesize speech.
- Save the audio file in the **Destination Bucket**.

### Step 8: Test the System
1. Upload a `.txt` file into the **Source Bucket**.
2. Check the **Destination Bucket** for the resulting `.mp3` file.

---

## Example Workflow

**Input**: Upload a `.txt` file to the Source S3 Bucket.
**Output**: Retrieve the corresponding audio file from the Destination S3 Bucket.

---

## Challenges & Best Practices

### Challenges
- **Text Length**: The AWS Free Tier allows a maximum file length of 3000 words using the **Standard Engine**.
- **Limited Voices**: The Free Tier supports fewer voice options.

### Best Practices
- Use proper IAM policies for secure access to S3 and Polly.
- Test with a variety of text files for compatibility.
- Upgrade to Polly’s **Neural Engine** or **Long-Form Engine** for better voice quality and longer file support.

---

## Project Structure

```plaintext
.
├── README.md         # Project documentation
├── lambda_function.py # Lambda function code
```

---

## FAQs

**1. How does Audify handle text-to-speech conversion?**  
When a `.txt` file is uploaded to the source S3 bucket, an event triggers the Lambda function. The function uses Amazon Polly to process the text and stores the audio file in the destination S3 bucket.

**2. Can I use advanced Polly engines?**  
Yes! You can upgrade to the **Neural Engine** or **Long-Form Engine** for enhanced voice quality and increased text limits.

**3. What are the limitations of the Free Tier?**  
- Maximum text length: 3000 words.
- Limited voice options.

---

## Conclusion

Audify brings written words to life, making content accessible and engaging for a wider audience. Whether you're an author, blogger, or educator, Audify transforms your storytelling journey into a more enriching experience.

### Ready to revolutionize your content?
Try **Audify** today and let your words find their voice!

---


## Author

**Mayuresh Muluk**  
Reach out with questions or feedback!
