```markdown
# Chaining Augmentation with PredictionGuard API

This project demonstrates how to download a website, split the content into chunks, and generate embeddings using the [PredictionGuard API](https://predictionguard.com). We use `go-client` to interact with the API, convert HTML content into Markdown, and store vectorized embeddings.

## Project Structure

- `main.go`: The main Go program that handles downloading the website, chunking the content, embedding the text, and saving the results into a JSON file.
- `chunks.json`: The output file that contains the vectorized embeddings of the website content.

## Prerequisites

1. **Go**: Make sure Go is installed. You can download it [here](https://golang.org/dl/).
2. **PredictionGuard API Key**: Set up an account at [PredictionGuard](https://predictionguard.com) and get your API key.

## Setup and Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/chaining-augmentation-02.git
   cd chaining-augmentation-02
   ```

2. **Initialize the Go Module**:
   ```bash
   go mod init chaining-augmentation-02
   ```

3. **Install Dependencies**:
   ```bash
   go mod tidy
   go get github.com/JohannesKaufmann/html-to-markdown
   go get github.com/predictionguard/go-client
   ```

4. **Set the PredictionGuard API Key**:
   Export your API key as an environment variable:
   ```bash
   export PGKEY="your_predictionguard_api_key"
   ```

## Running the Project

1. **Execute the Script**:
   The script will fetch a webpage, split its content into chunks, and generate embeddings.
   ```bash
   go run main.go
   ```

   You should see the following output in the terminal:
   ```
   Embedding chunk 1 of 59
   Embedding chunk 2 of 59
   ...
   ```

2. **Check the Output**:
   The vectorized embeddings will be stored in `chunks.json`:
   ```bash
   cat chunks.json
   ```

## Code Explanation

- **`websiteChunks` Function**: Downloads a webpage and converts the HTML into Markdown. It then splits the Markdown content into smaller chunks for embedding.
  
- **`embed` Function**: Sends chunks of text to the PredictionGuard API to generate embeddings. It supports embedding both text and images.
  
- **Chunking Logic**: The `characterTextSplitter` function splits the text into smaller, overlapping chunks to better handle embedding large documents.

## Troubleshooting

If you encounter an error related to the model not being supported (e.g., `"Hermes-2-Pro-Llama-3-8B"`), ensure you are using a valid model. Update the model name in the following line in `main.go`:

```go
resp, err := cln.Embedding(ctx, "text-embedding-ada-002", input)
```

You can find supported models in the PredictionGuard API documentation.