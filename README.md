# ml-design-doc: Support Request Categorization

---
## 1. Overview

The purpose of this design document is to outline the development of a machine learning-based solution for classifying customer support requests. The goal is to route tickets to the appropriate team accurately and adapt to new categories or types of queries. The solution will involve a pipeline for data ingestion, model training, evaluation, and retraining. Initially, model is going to be trained on support query datasets from HuggingFace, but I may run the finished version on real data from Jira Service Management support project I am running. 

## 2. Motivation
Automated routing and categorization of customer requests greatly improves operational efficiency (helps meet acceptance and first response SLAs), reduces costs (reduces the number of L1 support agents required) and in general makes day-to-day of support team easier since nobody likes to be on monitoring duty. 

## 3. Success metrics
- Increased accuracy in query classification.
- Reduced manual intervention in routing queries.
- Decreased average response time for customer queries.

## 4. Requirements & Constraints
### Functional Requirements
- The system should classify customer support queries with high accuracy. (definition of high is TBD)
- The system should provide regular reports on classification accuracy and performance.

### Non-Functional Requirements
- The system should handle a high volume of queries with low latency.
- It should comply with data privacy regulations such as GDPR.
- Cost of operation should be as low as possible since I am out of free credits/trials on most Cloud Providers

### Constraints
- System should be additionally adapted for each separate ITSM solution, as they have different architectures, APIs and data policies. 

### 4.1 What's in-scope & out-of-scope?
#### In scope
- Classification of customer support requests.
- Adaptation to new categories and query types.
- Regular evaluation and retraining of the model.

#### Out of scope
- Automated request processing and customer communication
## 5. Methodology

### 5.1. Problem statement

The problem is framed as a supervised classification task where the goal is to assign each customer support query to the most appropriate department based on its content.

### 5.2. Data

I have found a large number of interesting datasets on HuggingFace (and not much on Kaggle, surprisingly) that I am going to use as training data.

### 5.3. Techniques

- Data Preprocessing: Tokenization, stopword removal, and stemming/lemmatization.
- Feature Engineering: TF-IDF, word embeddings, or contextual embeddings (maybe BERT?).
- Model Selection: I am not entirely sure yet, but I will try to work with simple algorhytms first (Random Forests, XGBoost) and then implement Transformer-based architecture (Mistral Small 24B - https://huggingface.co/mistralai/Mistral-Small-24B-Instruct-2501)

### 5.4. Experimentation & Validation

- Offline Evaluation: Use metrics such as accuracy, precision, recall, and F1-score.
- A/B Testing: Assign treatment and control groups based on customer sessions. Measure success metrics such as classification accuracy and customer satisfaction scores. Guardrail metrics include query volume and system latency.

### 5.5. Human-in-the-loop

- Incorporate a feedback loop where misclassified queries are reviewed by human agents.
- Allow human agents to override model predictions and provide correct labels for retraining.

## 6. Implementation

### 6.1. High-level design

![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Data-flow-diagram-example.svg/1280px-Data-flow-diagram-example.svg.png)

Start by providing a big-picture view. [System-context diagrams](https://en.wikipedia.org/wiki/System_context_diagram) and [data-flow diagrams](https://en.wikipedia.org/wiki/Data-flow_diagram) work well.

### 6.2. Infra

How will you host your system? On-premise, cloud, or hybrid? This will define the rest of this section

### 6.3. Performance (Throughput, Latency)

How will your system meet the throughput and latency requirements? Will it scale vertically or horizontally?

### 6.4. Security

How will your system/application authenticate users and incoming requests? If it's publicly accessible, will it be behind a firewall?

### 6.5. Data privacy

How will you ensure the privacy of customer data? Will your system be compliant with data retention and deletion policies (e.g., [GDPR](https://gdpr.eu/what-is-gdpr/))?

### 6.6. Monitoring & Alarms

How will you log events in your system? What metrics will you monitor and how? Will you have alarms if a metric breaches a threshold or something else goes wrong?

### 6.7. Cost
How much will it cost to build and operate your system? Share estimated monthly costs (e.g., EC2 instances, Lambda, etc.)

### 6.8. Integration points

How will your system integrate with upstream data and downstream users?

### 6.9. Risks & Uncertainties

Risks are the known unknowns; uncertainties are the unknown unknows. What worries you and you would like others to review?

## 7. Appendix

### 7.1. Alternatives

#### Rule-based System
- Pros: Simple to implement, no need for large datasets.
- Cons: Limited adaptability to new query types, high maintenance.

#### Unsupervised Learning
- Pros: Can discover hidden patterns in data.
- Cons: Less control over classification outcomes, harder to evaluate.

### 7.2. Experiment Results

TBD

### 7.3. Performance benchmarks

TBD

### 7.4. Milestones & Timeline

TBD

### 7.5. Glossary

TBD

### 7.6. References

TBD

