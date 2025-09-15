# Lambda Deploy Pipeline

This project demonstrates **automated deployment of an AWS Lambda function** using **GitHub Actions**.

With this setup, whenever you push code to the `main` branch, your Lambda function is automatically updated without manual intervention.

---

## **Project Structure**

lambda-deploy-pipeline/
│
├── lambda_function.py # Your Lambda function code
├── requirements.txt # Python dependencies (can be empty)
├── README.md # This documentation
└── .github/
└── workflows/
└── lambda-deploy.yml # GitHub Actions workflow

markdown
Copy code

---

## **Manual AWS Setup (One-Time)**

1. **Create a Lambda function**  
   - Go to AWS Console → Lambda → Create function → Author from scratch  
   - Runtime: Python 3.9  
   - Function name: `lambda_function` (or your preferred name)  
   - Note the **Handler** must be `lambda_function.lambda_handler`  

2. **Create an IAM user for GitHub Actions**  
   - Access type: Programmatic access  
   - Attach a policy with `lambda:UpdateFunctionCode` permissions  
   - Copy **Access Key ID** and **Secret Access Key**

3. **Add GitHub Secrets** to your repository  
   - `AWS_ACCESS_KEY_ID`  
   - `AWS_SECRET_ACCESS_KEY`  
   - `AWS_REGION` → `us-east-1`  
   - `LAMBDA_FUNCTION_NAME` → the Lambda function name  

---

## **How the Workflow Works**

1. Push code to the `main` branch  
2. GitHub Actions workflow is triggered  
3. Workflow packages your Lambda function + dependencies  
4. AWS credentials are configured  
5. The Lambda function code is updated automatically  

---

## **Testing Lambda**

- **AWS Console:** Lambda → Test → Create a test event → Run → Check response  
- **Expected output:**  
```json
{
  "statusCode": 200,
  "body": "Hello from Lambda Deploy Pipeline!"
}
Notes
If your Lambda uses external packages, list them in requirements.txt

Ensure the file name and Handler match (lambda_function.lambda_handler)

Logs appear in GitHub Actions and AWS CloudWatch for debugging
