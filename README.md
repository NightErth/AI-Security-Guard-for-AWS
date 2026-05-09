
# Build an AI Security Guard for AWS


**Author:** NightErth

---

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/ai-aws-security-guard_aws2m3n4o)

---

## Introducing Today's Project!

Project Motivation

In this project, I’m building a Python-based AWS security scanner to identify potential misconfiguration in Amazon S3 buckets and to experiment with AWS MCP for monitoring and automation. The goal is to get hands-on experience with how cloud security checks actually work in practice, rather than just reading about them.

I’m particularly interested in this area because S3 misconfiguration have been behind several major security incidents in the past. Many of these issues were preventable, which makes them even more relevant to study. By working on this project, I want to better understand how these mistakes happen and how they can be detected and fixed early.

Overall, this project is a way for me to build practical skills in AWS security, improve how I approach identifying risks, and get more comfortable with applying security best practices in real-world scenarios.

### Key tools and concepts


Tools Used:
Cursor: AI-powered tool for interacting with AWS services and automating tasks through natural language.
MCP (Managed Cloud Platform): Integrated with Cursor for managing AWS resources and automating security tasks.
AWS: Amazon Web Services, used to host and configure S3 buckets for testing and remediation.
Python: Programming language used to write the security scanner (scanner.py) and automate the process of detecting and fixing security issues.
Key Concepts Learned:
AWS S3 Security (Public Access Blocks): I gained a deeper understanding of the importance of configuring Public Access Blocks to prevent unauthorized access to S3 buckets. I learned how to detect and remediate misconfigurations that could lead to data exposure or breaches.
Error Handling with try and except: I learned how to handle potential errors in API calls and AWS interactions to ensure the security scanner runs smoothly without crashing, even when encountering misconfigured or inaccessible resources.

### Challenges and wins

Time Spent:

This project took approximately 3 hours to complete, from setting up the environment to testing and remediating the security issues.

Challenges Faced:

The most challenging part of the project was configuring my AWS credentials correctly. Ensuring proper access permissions and setting up the connection between my local environment and AWS required troubleshooting and multiple adjustments to ensure everything was working smoothly.

Most Rewarding Part:

The most rewarding aspect was successfully fixing the AWS S3 bucket security issues. Using the scanner to detect vulnerabilities and then applying automated remediation through Cursor and AWS MCP was both satisfying and educational. It reinforced the importance of automating security checks and fixes in cloud environments, ensuring that vulnerabilities are addressed promptly.

### Why I did this project

Project Motivation and Goals

I undertook this project today with the goal of learning how to manage AWS security using AI. Specifically, I wanted to explore the integration of boto3 for scripting manual AWS security checks and AWS MCP for real-time fixes and queries powered by AI.

This project successfully met my objectives by allowing me to:

Analyze the use of boto3 for performing detailed, manual security checks on AWS resources like S3 buckets.
Leverage AWS MCP to enable AI-powered remediation and immediate security updates, demonstrating the power of AI to automate cloud security tasks.

By completing this project, I gained practical experience in combining these tools to enhance AWS security, giving me a deeper understanding of both manual and automated cloud security management.

---

## Setting Up Your Environment

Environment Setup

In this step, I set up the local development environment required to interact with AWS services. This includes installing Python, configuring the AWS CLI, setting up AWS credentials, and installing necessary dependencies such as boto3 and UV. I also create a dedicated project directory to organize the codebase.

This setup is essential for enabling authenticated communication with Amazon S3 and other AWS resources. With these components in place, I can programmatically access and analyze S3 buckets as part of the security scanning process.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/ai-aws-security-guard_aws2c3d4e)

Verification

To confirm that the environment was set up correctly, I verified the installation of boto3 by running:

pip list | Select-String boto3

The output displayed version 1.43.1, confirming that the package was successfully installed and available in the environment.

---

## Building the S3 Security Scanner

Public Access Security Check

In this step, I build a security scanner to detect public access misconfigurations across Amazon S3 buckets within my AWS account. The scanner evaluates bucket-level permissions to identify resources that may be unintentionally exposed to the public.

The objective is to proactively detect potential security risks and address them early, reducing the likelihood of data exposure. By automating this check, I can continuously monitor for misconfigurations instead of relying on manual reviews.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/ai-aws-security-guard_aws5f6g7h)

How the Scanner Works and What I Built

The scanner is a Python-based script that analyzes all Amazon S3 buckets within an AWS account to detect potential public access misconfigurations.

It works by first retrieving a list of all available S3 buckets using the AWS SDK for Python (boto3). The script then iterates through each bucket and checks the bucket’s Public Access Block configuration against the four key security controls:

***BlockPublicAcls***<br>
***BlockPublicPolicy***<br>
***IgnorePublicAcls***<br>
***RestrictPublicBuckets***<br>

If any of these settings are missing or disabled, the bucket is flagged as a potential security risk and recorded as a critical finding.

The implementation also includes structured error handling using try/except blocks. This is used to manage both AWS-specific errors (such as missing Public Access Block configurations) and unexpected runtime exceptions. Without this error handling, the scanner could fail or terminate prematurely when encountering misconfigured or restricted buckets.

---

## Connecting Cursor to AWS with MCP

Connecting Cursor to AWS

In this step, I configure Cursor to integrate with AWS by setting up the AWS MCP connection within the editor. This involves updating the MCP configuration, restarting Cursor, and verifying that the connection is successfully established.

The purpose of this setup is to enable interaction with AWS MCP directly through Cursor’s chat interface. Once connected, I can execute and manage AWS-related operations more efficiently from within the development environment, improving both workflow and productivity during the security scanning process.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/ai-aws-security-guard_aws8i9j0k)

MCP Connection Setup and Verification

I configured the integration by adding the AWS MCP settings in Cursor’s mcp.json configuration file. After completing the setup, I restarted Cursor to apply the changes.

To verify the connection, I checked the MCP settings page within Cursor. This confirmed that the AWS MCP server was successfully connected and available for use within the development environment.

---

## Testing Your Scanner

Testing the Security Scanner

In this step, I test the security scanner by creating a deliberately misconfigured Amazon S3 bucket to simulate a real-world security issue. This controlled setup allows me to validate that the scanner correctly identifies public access misconfigurations.

The goal is to ensure that the scanner.py script can reliably detect critical issues in a realistic scenario. By introducing a known misconfiguration, I can confirm that the detection logic works as expected and that high-severity findings are properly reported.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/ai-aws-security-guard_aws2m3n4o)

I created a test bucket using AWS MCP through Cursor’s AI chat interface, intentionally leaving it misconfigured to simulate a real-world security issue in Amazon S3.

After running scanner.py, the script returned the following finding:

CRITICAL: [test-security-demo-33333] No public access block configured.

This result confirms that the scanner is functioning as intended, successfully identifying a critical misconfiguration. Specifically, the absence of a Public Access Block setting exposes the bucket to potential unauthorized access, representing a significant security risk.

---

## Fixing Security Issues with AI

Automating Remediation with AI

In this step, I use Cursor's AI-powered interface integrated with AWS MCP to automatically remediate the security issues detected in the test S3 bucket. By leveraging natural language commands, I instruct the system to apply the necessary Public Access Block configuration, effectively resolving the security flaw.

This approach aligns with professional tools, where detecting security issues is only half the battle. It is equally important to quickly and consistently fix vulnerabilities. By using Cursor’s integration with AWS MCP, I can not only identify misconfigurations but also implement corrections through natural language, streamlining the remediation process.

This AI-driven remediation reduces the risk of human error and ensures security settings are applied promptly, enhancing the overall security posture of cloud resources.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/ai-aws-security-guard_awssec2b3c)

Remediation Process with Cursor and AWS MCP

After detecting security issues using the scanner.py script on my purposely misconfigured S3 bucket, I leveraged Cursor’s AI chat interface to automatically resolve the identified issues. Specifically, the scanner flagged the bucket with the issue: "Public access block not configured."

To remediate the problem, I prompted Cursor's AI chat to investigate and address the misconfiguration. Using natural language commands, Cursor interacted with AWS MCP via API calls to apply the necessary Public Access Block settings to the faulty bucket. This automated process fixed the security flaw by ensuring that public access was properly restricted.

By using Cursor’s AI-powered interface, I was able to quickly and efficiently resolve the vulnerability, demonstrating the value of automated remediation in cloud security.

---

